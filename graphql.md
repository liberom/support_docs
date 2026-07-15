# GraphQL.org Website

GraphQL.org is the official website and documentation hub for GraphQL, built as a modern Next.js application. The site serves as the primary resource for GraphQL developers worldwide, providing comprehensive documentation, interactive code examples, conference information, and community resources. It features a documentation system powered by Nextra with MDX support, interactive GraphQL playgrounds using CodeMirror, and a complete conference management system.

The website architecture combines Next.js 14 App Router with file-based routing, React Server Components, and static site generation. Content is authored in MDX (Markdown with JSX), enabling rich interactive documentation with embedded React components. The build system integrates automated GitHub statistics fetching, library sorting algorithms, conference schedule synchronization from Sched API, and RSS feed generation. The site is deployed via Vercel with automatic builds from the `source` branch.

## Development and Build

### Local development server
Start the development server with hot-reloading for instant feedback during development.

```bash
# Clone and setup
git clone https://github.com/graphql/graphql.github.io.git
cd graphql.github.io
pnpm install

# Start development server
pnpm dev
# Server runs at http://localhost:3000
```

### Production build
Build the static site for deployment with optimized assets and pre-rendered pages.

```bash
# Full production build with GitHub stats
pnpm build
# Runs prebuild script (GitHub stats) then builds and generates sitemap

# Start production server
pnpm start

# Analyze bundle size
pnpm analyze
# Or use environment variable
ANALYZE=true pnpm build
```

### Testing and validation
Validate content integrity and run end-to-end tests to ensure quality.

```bash
# Run all tests (Playwright E2E + unit tests)
pnpm test

# Run E2E tests only
pnpm test:e2e

# Run unit tests only
pnpm test:unit

# Interactive test UI
pnpm test:ui

# Check for broken links in documentation
pnpm check:links

# Validate GraphQL code snippets
pnpm validate:snippets

# Linting
pnpm lint
pnpm lint:docs

# Formatting
pnpm format:check
pnpm format
```

## RSS Feed Generation

### Blog RSS feed route
Generate an RSS feed from blog posts with automatic frontmatter extraction and content summarization.

```typescript
// src/app/blog/rss.xml/route.ts
import fs from "node:fs/promises"
import path from "node:path"
import { compileMdx } from "nextra/compile"
import { toString } from "hast-util-to-string"
import RSS from "rss"

const SITE_URL = "https://graphql.org"

const rehypeEnhanceFrontmatter: Plugin<[], Root> = () => (tree, file) => {
  const { frontMatter } = file.data as {
    frontMatter: Record<string, string | Date>
  }

  // Filter out code blocks from description
  tree = {
    ...tree,
    children: tree.children.filter(node => (node as any).tagName !== "pre"),
  }

  const [filePath] = file.history

  frontMatter.description = toString(tree as any).trimStart()
  frontMatter.fileName = path.parse(filePath).name
  frontMatter.date = new Date(frontMatter.date)
}

export async function GET() {
  const files = await fs.readdir("./src/pages/blog")

  const blogs = await Promise.all(
    files
      .filter(filename => /\.mdx?$/.test(filename))
      .map(async filename => {
        const filePath = path.join("./src/pages/blog", filename)
        const content = await fs.readFile(filePath, "utf8")
        return await compileMdx(content, {
          filePath,
          mdxOptions: {
            rehypePlugins: [rehypeEnhanceFrontmatter],
          },
        })
      }),
  )

  blogs.sort((a, b) => b.frontMatter.date - a.frontMatter.date)

  const feed = new RSS({
    title: "Blog | GraphQL",
    description: "Blog | GraphQL",
    generator: "Next.js",
    feed_url: `${SITE_URL}/blog/rss.xml`,
    site_url: SITE_URL,
    copyright: `Copyright © ${new Date().getFullYear()} The GraphQL Foundation. All rights reserved.`,
    language: "en-US",
    pubDate: blogs[0].frontMatter.date.toUTCString(),
    ttl: 60,
  })

  for (const { frontMatter } of blogs) {
    feed.item({
      title: frontMatter.title,
      description: frontMatter.description.slice(0, 139) + "…",
      url: `${SITE_URL}/blog/${frontMatter.fileName}`,
      categories: frontMatter.tags,
      author: frontMatter.byline,
      date: frontMatter.date.toUTCString(),
    })
  }

  return new Response(feed.xml({ indent: true }), {
    headers: {
      "Content-Type": "application/xml; charset=utf-8",
    },
  })
}
```

## Library Sorting Algorithm

### Sort libraries by metrics
Rank GraphQL libraries using a weighted scoring system based on downloads, GitHub stars, activity, and community engagement.

```typescript
// scripts/sort-libraries/sort-libraries.ts
export interface Library {
  name: string
  description: string
  howto: string
  url: string
  github: string | undefined
  npm: string | undefined
  gem: string | undefined
  sourcePath: string
}

export async function sortLibs(
  libraries: Library[],
): Promise<{ sortedLibs: Library[]; totalStars: number }> {
  let totalStars = 0
  const libsWithScores = await Promise.all(
    libraries.map(async lib => {
      const [npmStats, gemStars, githubStats, httpScore] = await Promise.all([
        lib.npm ? getNpmStats(lib.npm) : undefined,
        lib.gem ? getGemStats(lib.gem) : undefined,
        lib.github ? getGitHubStats(lib.github) : undefined,
        lib.name ? getHttpScore(lib.name) : undefined,
      ])

      const result = {
        ...lib,
        downloadCount: npmStats ?? gemStars ?? 0,
        stars: githubStats?.stars ?? 0,
        httpScore: httpScore ?? 0,
        ...githubStats,
      }
      totalStars += result.stars
      return result
    }),
  )

  const sortedLibs = libsWithScores.sort((a, b) => {
    let aScore = 0,
      bScore = 0

    // Downloads worth 36 points
    if (a.downloadCount > b.downloadCount) {
      aScore += 36
    } else if (b.downloadCount > a.downloadCount) {
      bScore += 36
    }

    // HTTP score worth 10 points
    if (a.httpScore > b.httpScore) {
      aScore += 10
    } else if (b.httpScore > a.httpScore) {
      bScore += 10
    }

    // Recent commits worth 28 points
    if ("hasCommitsInLast3Months" in a && a.hasCommitsInLast3Months) {
      aScore += 28
    }
    if ("hasCommitsInLast3Months" in b && b.hasCommitsInLast3Months) {
      bScore += 28
    }

    // Stars worth 36 points
    if (a.stars > b.stars) {
      aScore += 36
    } else if (a.stars < b.stars) {
      bScore += 36
    }

    if (bScore > aScore) {
      return 1
    }
    if (bScore < aScore) {
      return -1
    }
    return 0
  })

  return { sortedLibs, totalStars }
}
```

## Conference Schedule Sync

### Sync conference data from Sched
Synchronize conference schedules and speaker data from Sched API with intelligent change detection and quota management.

```bash
# Sync schedule for specific year (default: current year)
tsx scripts/sync-sched/sync.ts --year 2025 --quota 10

# Environment variable required
export SCHED_ACCESS_TOKEN_2025="your-token-here"

# Show help
tsx scripts/sync-sched/sync.ts --help
```

```typescript
// scripts/sync-sched/sync.ts
import assert from "node:assert"
import { parseArgs } from "node:util"
import { join } from "node:path"
import { readFile, writeFile } from "node:fs/promises"
import pLimit from "p-limit"

import {
  getSchedule,
  getSpeakerDetails,
  getSpeakers,
  mergeSpeaker,
  RequestContext,
} from "@/app/conf/_api/sched-client"
import type { ConferenceYear, SchedSpeaker } from "@/app/conf/_api/sched-types"

const DEFAULT_SPEAKER_DETAILS_REQUEST_QUOTA = 10

async function sync(
  year: ConferenceYear,
  detailsRequestsQuota: number,
  token: string,
) {
  const apiUrl = {
    2023: "https://graphqlconf23.sched.com/api",
    2024: "https://graphqlconf2024.sched.com/api",
    2025: "https://graphqlconf2025.sched.com/api",
  }[year]

  assert(apiUrl, `API URL for year ${year} not found`)

  const ctx: RequestContext = { apiUrl, token }

  const speakersFilePath = join(import.meta.dirname, "speakers.json")
  const scheduleFilePath = join(import.meta.dirname, `schedule-${year}.json`)

  console.log("Getting schedule and speakers list...")

  // Fetch current and existing data in parallel
  const schedule = getSchedule(ctx)
  const thisYearSpeakers = getSpeakers(ctx)
  const existingSchedule = readFile(scheduleFilePath, "utf-8").then(JSON.parse)
  const existingSpeakers = readFile(speakersFilePath, "utf-8").then(JSON.parse)

  // Compare and detect changes
  const scheduleComparison = compare(await existingSchedule, await schedule, "id")
  const speakerComparison = compare(
    await existingSpeakers.then(data => data.speakers),
    await thisYearSpeakers.then(speakers => speakers.map(s => ({
      ...s,
      _years: [year],
    }))),
    "username",
    { merge: mergeSpeaker }
  )

  // Fetch additional details for speakers (respecting quota)
  const toUpdate = allSpeakers
    .filter(x => x._years?.includes(year))
    .sort((a, b) => (a["~syncedDetailsAt"] ?? 0) - (b["~syncedDetailsAt"] ?? 0))
    .slice(0, detailsRequestsQuota)

  await Promise.all(
    toUpdate.map(speaker => getSpeakerDetails(ctx, speaker.username))
  )

  // Write updated data
  await writeFile(scheduleFilePath, JSON.stringify(await schedule, null, 2))
  await writeFile(speakersFilePath, JSON.stringify({ equal, speakers: updatedSpeakers }, null, 2))
}
```

## Code Data Update System

### Parse and organize code examples
Extract frontmatter metadata from markdown files and organize libraries by language, category, and tool type.

```typescript
// scripts/update-code-data/update-code-data.ts
import { readFile } from "fs/promises"
import { promisify } from "util"
import * as frontmatterParser from "parser-front-matter"
import { Library } from "../sort-libraries/sort-libraries"

const parse$ = promisify(frontmatterParser.parse)

export type CodeData = {
  Languages: {
    [languageName: string]: {
      [categoryName: string]: Library[]
    }
  }
  Tools: {
    [toolName: string]: {
      [categoryToolsName: string]: Library[]
    }
  }
  Services: Library[]
}

export async function updateCodeData(
  markdownFilePaths: string[],
  slugMap: string,
): Promise<CodeData> {
  const codeData = {} as CodeData
  await Promise.all(
    markdownFilePaths.map(async markdownFilePath => {
      const markdownFileContent = await readFile(markdownFilePath, "utf-8")
      let {
        data: { name, description, url, github, npm, gem },
        content: howto,
      } = await parse$(markdownFileContent)
      howto = howto.trim()
      const pathArr = markdownFilePath.split("/")
      const languageSupport = markdownFilePath.includes("language-support")
      const toolsSupport = markdownFilePath.includes("tools")

      switch (true) {
        case languageSupport: {
          const languageSupportDirIndex = pathArr.indexOf("language-support")
          const languageNameSlugIndex = languageSupportDirIndex + 1
          const languageNameSlug = pathArr[languageNameSlugIndex]
          const languageName = slugMap[languageNameSlug]
          codeData.Languages ||= {}
          codeData.Languages[languageName] ||= {}

          const categoryNameSlugIndex = languageSupportDirIndex + 2
          const categoryNameSlug = pathArr[categoryNameSlugIndex]
          const categoryName = slugMap[categoryNameSlug]
          codeData.Languages[languageName][categoryName] ||= []
          codeData.Languages[languageName][categoryName].push({
            name,
            description,
            howto,
            url,
            github,
            npm,
            gem,
            sourcePath: markdownFilePath,
          })
          break
        }
        case toolsSupport: {
          const toolSupportDirIndex = pathArr.indexOf("tools")
          const toolNameSlugIndex = toolSupportDirIndex + 1
          const toolNameSlug = pathArr[toolNameSlugIndex]
          const toolName = slugMap[toolNameSlug]
          codeData.Tools ||= {}
          codeData.Tools[toolName] ||= {}
          const categoryToolsNameSlugIndex = toolSupportDirIndex + 2
          const categoryToolsNameSlug = pathArr[categoryToolsNameSlugIndex]
          const categoryToolsName = slugMap[categoryToolsNameSlug]
          codeData.Tools[toolName][categoryToolsName] ||= []

          codeData.Tools[toolName][categoryToolsName].push({
            name,
            description,
            howto,
            url,
            github,
            npm,
            gem,
            sourcePath: markdownFilePath,
          })
          break
        }
        default: {
          const codeDirIndex = pathArr.indexOf("code")
          const categoryNameSlugIndex = codeDirIndex + 1
          const categoryNameSlug = pathArr[categoryNameSlugIndex]
          const categoryName = slugMap[categoryNameSlug]
          codeData[categoryName] ||= []
          codeData[categoryName].push({
            name,
            description,
            howto,
            url,
            github,
            npm,
            gem,
            sourcePath: markdownFilePath,
          })
        }
      }
    }),
  )
  return codeData
}
```

## GraphQL Schema and Resolvers

### Interactive Star Wars schema
Complete executable schema with resolvers for the interactive GraphQL playground on the website.

```typescript
// src/components/interactive-code-block/swapi-schema.tsx
import { makeExecutableSchema } from "@graphql-tools/schema"

const typeDefs = /* GraphQL */ `
  schema {
    query: Query
    mutation: Mutation
  }

  "The query type, represents all of the entry points into our object graph"
  type Query {
    hero(episode: Episode): Character
    reviews(episode: Episode!): [Review]
    search(text: String): [SearchResult]
    character(id: ID!): Character
    droid(id: ID!): Droid
    human(id: ID!): Human
    starship(id: ID!): Starship
  }

  "The mutation type, represents all updates we can make to our data"
  type Mutation {
    createReview(episode: Episode, review: ReviewInput!): Review
    rateFilm(episode: Episode!, rating: FilmRating!): Film
    updateHumanName(id: ID!, name: String!): Human
    deleteStarship(id: ID!): ID
  }

  "The episodes in the Star Wars trilogy"
  enum Episode {
    "Star Wars Episode IV: A New Hope, released in 1977."
    NEWHOPE
    "Star Wars Episode V: The Empire Strikes Back, released in 1980."
    EMPIRE
    "Star Wars Episode VI: Return of the Jedi, released in 1983."
    JEDI
  }

  "A character from the Star Wars universe"
  interface Character {
    "The ID of the character"
    id: ID!
    "The name of the character"
    name: String!
    "The friends of the character, or an empty list if they have none"
    friends: [Character]
    "The friends of the character exposed as a connection with edges"
    friendsConnection(first: Int, after: ID): FriendsConnection!
    "The movies this character appears in"
    appearsIn: [Episode]!
  }

  "Units of height"
  enum LengthUnit {
    "The standard unit around the world"
    METER
    "Primarily used in the United States"
    FOOT
  }

  "A humanoid creature from the Star Wars universe"
  type Human implements Character {
    id: ID!
    name: String!
    height(unit: LengthUnit = METER): Float
    mass: Float
    friends: [Character]
    friendsConnection(first: Int, after: ID): FriendsConnection!
    appearsIn: [Episode]!
    starships: [Starship]
  }

  type Droid implements Character {
    id: ID!
    name: String!
    friends: [Character]
    friendsConnection(first: Int, after: ID): FriendsConnection!
    appearsIn: [Episode]!
    primaryFunction: String
  }
`

const resolvers = {
  Query: {
    hero: (root, { episode }) => {
      if (episode === "EMPIRE") return humanData["1000"] // Luke
      return droidData["2001"] // R2-D2
    },
    character: (root, { id }) => humanData[id] || droidData[id],
    human: (root, { id }) => humanData[id],
    droid: (root, { id }) => droidData[id],
    starship: (root, { id }) => starshipData[id],
    search: (root, { text }) => {
      // Search implementation across humans, droids, and starships
      const regexp = new RegExp(text, "i")
      return [...Object.values(humanData), ...Object.values(droidData),
              ...Object.values(starshipData)].filter(obj => regexp.test(obj.name))
    },
  },
  Mutation: {
    createReview: (root, { episode, review }) => review,
    updateHumanName: (root, { id, name }) => {
      const human = humanData[id]
      if (!human) throw new Error("Human not found")
      return { ...human, name }
    },
    deleteStarship: (root, { id }) => {
      if (!starshipData[id]) throw new Error("Starship not found")
      delete starshipData[id]
      return id
    },
  },
  Human: {
    height: ({ height }, { unit }) => {
      if (unit === "FOOT") return height * 3.28084
      return height
    },
    friends: ({ friends }) => friends.map(id => humanData[id] || droidData[id]),
    starships: ({ starships }) => starships.map(id => starshipData[id]),
  },
  Droid: {
    friends: ({ friends }) => friends.map(id => humanData[id] || droidData[id]),
  },
}

export const StarWarsSchema = makeExecutableSchema({ typeDefs, resolvers })
```

## Next.js Configuration

### Custom webpack and MDX configuration
Configure Next.js with Nextra for MDX documentation, custom SVG handling, and image optimization.

```javascript
// next.config.js
import nextra from "nextra"
import path from "node:path"
import withLess from "next-with-less"
import nextBundleAnalyzer from "@next/bundle-analyzer"
import fs from "fs"
import rehypeMermaid from "rehype-mermaid"
import withPlaiceholder from "@plaiceholder/next"

import { remarkGraphiQLComment } from "./src/remark-graphiql-comment.js"
import { syntaxHighlightingThemes } from "./src/_design-system/syntax/index.js"

const vercelJSON = JSON.parse(fs.readFileSync("./vercel.json", "utf-8"))

const withNextra = nextra({
  autoImportThemeStyle: false,
  theme: "nextra-theme-docs",
  themeConfig: "./theme.config.tsx",
  mdxOptions: {
    remarkPlugins: [remarkGraphiQLComment],
    rehypePlugins: [mermaidConfig()],
    rehypePrettyCodeOptions: {
      theme: syntaxHighlightingThemes,
    },
  },
})

const sep = path.sep === "/" ? "/" : "\\\\"
const ALLOWED_SVG_REGEX = new RegExp(`${sep}icons${sep}.+\\.svg$`)

const config = {
  webpack(config) {
    // MDX with ?raw query for raw content
    const mdxRule = config.module.rules.find(rule => rule.test?.test?.(".mdx"))
    if (mdxRule) {
      mdxRule.resourceQuery = { not: /raw/ }
    }
    config.module.rules.push({
      test: /\.mdx$/i,
      resourceQuery: /raw/,
      type: "asset/source",
    })

    // SVG handling with @svgr/webpack
    const fileLoaderRule = config.module.rules.find(rule =>
      rule.test?.test?.(".svg"),
    )
    fileLoaderRule.exclude = /\.svg$/i

    config.module.rules.push(
      {
        test: ALLOWED_SVG_REGEX,
        use: ["@svgr/webpack"],
      },
      {
        test: /\.svg$/i,
        exclude: ALLOWED_SVG_REGEX,
        resourceQuery: /svgr/,
        use: [{
          loader: "@svgr/webpack",
          options: {
            typescript: true,
            svgoConfig: {
              plugins: [
                {
                  name: "preset-default",
                  params: {
                    overrides: {
                      minifyStyles: false,
                      removeViewBox: false,
                      removeTitle: false,
                    },
                  },
                },
                "removeXMLNS",
                "removeXlink",
                "prefixIds",
              ],
            },
          },
        }],
      },
      {
        ...fileLoaderRule,
        test: /\.svg$/i,
        exclude: ALLOWED_SVG_REGEX,
        resourceQuery: {
          not: [...fileLoaderRule.resourceQuery.not, /svgr/],
        },
      },
    )

    return config
  },
  images: {
    remotePatterns: [{ hostname: "avatars.sched.co", pathname: "**" }],
  },
  env: {
    NEXT_PUBLIC_GA_ID: process.env.NODE_ENV === "production" ? "UA-44373548-16" : "",
  },
  headers: async () => {
    return [{
      source: "/graphql",
      headers: [
        { key: "Access-Control-Allow-Origin", value: "*" },
        { key: "Access-Control-Allow-Methods", value: "GET, POST, OPTIONS" },
        { key: "Access-Control-Allow-Headers", value: "Content-Type" },
      ],
    }]
  },
  trailingSlash: true,
  redirects: () => vercelJSON.redirects.filter(o => o.statusCode !== 200),
  async rewrites() {
    return [
      { source: "/swapi-graphql/:path*", destination: "https://swapi-graphql.netlify.app/:path*" },
      { source: "/graphql", destination: "https://swapi-graphql.netlify.app/graphql" },
    ]
  },
  typedRoutes: true,
}

const withBundleAnalyzer = nextBundleAnalyzer({
  enabled: process.env.ANALYZE === "true",
})

export default withBundleAnalyzer(withLess(withNextra(withPlaiceholder(config))))

function mermaidConfig() {
  return [
    rehypeMermaid,
    {
      mermaidConfig: {
        fontFamily: "var(--font-sans)",
        theme: "null",
        look: "classic",
        flowchart: {
          defaultRenderer: "elk",
          padding: 6,
        },
        themeCSS: `
          .node rect {
            fill: var(--mermaid-node-fill);
            stroke: var(--mermaid-node-stroke);
          }
          .label text, span {
            fill: hsl(var(--color-neu-900));
            color: hsl(var(--color-neu-900));
          }
          .flowchart-link {
            stroke: var(--mermaid-arrow);
          }
          .marker {
            stroke: var(--mermaid-arrow);
            fill: var(--mermaid-arrow);
          }
        `,
      },
    },
  ]
}
```

## Theme Configuration

### Nextra theme customization
Configure the documentation theme with custom branding, navigation, and SEO metadata.

```typescript
// theme.config.tsx
import { DocsThemeConfig, useConfig } from "nextra-theme-docs"
import { useRouter } from "next/router"

import { Navbar } from "@/components/navbar/navbar"
import { mdxComponents } from "@/_design-system/mdx-components"
import { GraphQLWordmarkLogo } from "@/icons"
import { Footer } from "@/components/footer"
import { NextraMdxWrapper } from "@/components/nextra-mdx-wrapper"
import { ThemeSwitch } from "@/components/theme-switch"

const graphQLLogo = (
  <GraphQLWordmarkLogo className="nextra-logo h-6" title="GraphQL" />
)

export default {
  backgroundColor: {
    light: "251,251,249",
    dark: "15,15,12",
  },
  head: function useHead() {
    const { frontMatter, title: pageTitle } = useConfig()
    const { asPath } = useRouter()

    const title = `${pageTitle}${asPath === "/" ? "" : " | GraphQL"}`
    const { description, canonical, image } = frontMatter
    return (
      <>
        <title>{title}</title>
        <meta property="og:title" content={title} key="meta-og-title" />
        {description && (
          <>
            <meta
              name="description"
              content={description}
              key="meta-description"
            />
            <meta
              property="og:description"
              content={description}
              key="meta-og-description"
            />
          </>
        )}
        {canonical && <link rel="canonical" href={canonical} />}
        {image && <meta name="og:image" content={image} />}
        <meta property="og:image" content="/img/og-image.png" />
        <meta property="twitter:site" content="@graphql" />
      </>
    )
  },
  logo: graphQLLogo,
  docsRepositoryBase: "https://github.com/graphql/graphql.github.io/tree/source",
  color: {
    hue: 319,
    lightness: {
      light: 44.1,
      dark: 90,
    },
  },
  sidebar: {
    defaultMenuCollapseLevel: 1,
  },
  footer: {
    component: () => <Footer />,
    content: "Copyright © 2025 The GraphQL Foundation. All rights reserved.",
  },
  navbar: {
    component: Navbar,
    extraContent: (
      <ThemeSwitch lite className="max-lg:hidden [&_span]:hidden" />
    ),
  },
  toc: {
    backToTop: true,
  },
  search: {
    placeholder: "Search…",
  },
  components: { ...mdxComponents, wrapper: NextraMdxWrapper },
} satisfies DocsThemeConfig
```

## GraphQL.org serves as the authoritative resource for GraphQL documentation, combining static content generation with dynamic interactive features. The site architecture enables efficient content management through MDX, automated data synchronization from external APIs, and sophisticated library ranking algorithms. Integration with external services like Sched for conference management and GitHub for repository statistics ensures content remains current. The development workflow supports hot-reloading for rapid iteration, comprehensive testing with Playwright, and automated link checking to maintain content quality.

The project exemplifies modern static site generation with Next.js, leveraging React Server Components for optimal performance, file-based routing for intuitive navigation, and extensive customization through Nextra. Content contributors can author documentation in Markdown while developers can extend functionality through React components, custom webpack loaders, and plugin integrations. The build pipeline orchestrates multiple data sources, transformations, and optimizations to deliver a fast, accessible, and feature-rich documentation experience for the global GraphQL community.
