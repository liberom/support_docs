# TypeScript Compiler API

TypeScript is a typed superset of JavaScript that compiles to clean JavaScript output. It provides optional static typing, classes, and interfaces for application-scale JavaScript development. The TypeScript compiler (`tsc`) analyzes TypeScript and JavaScript code, performs type checking, and emits standards-compliant JavaScript that runs in any browser, on any host, and on any operating system.

The TypeScript package exposes a powerful Compiler API that allows developers to programmatically compile, analyze, and transform TypeScript code. The API provides access to the full compiler pipeline including parsing, binding, type checking, and code emission. This enables building custom tools such as linters, documentation generators, code transformers, IDE integrations, and language services that leverage TypeScript's type system.

## Installation

Install TypeScript from npm to use the compiler and its API.

```bash
# Install TypeScript as a dev dependency
npm install -D typescript

# Or install globally
npm install -g typescript

# For nightly builds with latest features
npm install -D typescript@next

# Link TypeScript for API usage
npm link typescript

# Install Node.js types for API examples
npm install -D @types/node
```

## tsc - TypeScript Compiler CLI

The `tsc` command-line tool compiles TypeScript files to JavaScript with full type checking.

```bash
# Compile a single file
tsc app.ts

# Compile with specific target and module system
tsc app.ts --target ES2020 --module CommonJS

# Compile entire project using tsconfig.json
tsc

# Watch mode for development
tsc --watch

# Generate declaration files
tsc --declaration --emitDeclarationOnly

# Check types without emitting output
tsc --noEmit

# Initialize a new tsconfig.json
tsc --init

# Compile with strict mode enabled
tsc --strict app.ts

# Show all compiler options
tsc --help --all
```

## tsconfig.json Configuration

Configure TypeScript compilation options for a project using `tsconfig.json`.

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "CommonJS",
    "lib": ["ES2020", "DOM"],
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "declaration": true,
    "declarationMap": true,
    "sourceMap": true,
    "noImplicitAny": true,
    "strictNullChecks": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"]
    }
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist"]
}
```

## ts.createProgram() - Create Compilation Program

Create a Program instance representing the TypeScript compilation context for a set of files.

```typescript
import * as ts from "typescript";

function compile(fileNames: string[], options: ts.CompilerOptions): void {
  // Create a Program from the file names and options
  const program = ts.createProgram(fileNames, options);

  // Emit compiled JavaScript files
  const emitResult = program.emit();

  // Get all diagnostics (errors and warnings)
  const allDiagnostics = ts
    .getPreEmitDiagnostics(program)
    .concat(emitResult.diagnostics);

  // Process and display diagnostics
  allDiagnostics.forEach(diagnostic => {
    if (diagnostic.file) {
      const { line, character } = ts.getLineAndCharacterOfPosition(
        diagnostic.file,
        diagnostic.start!
      );
      const message = ts.flattenDiagnosticMessageText(diagnostic.messageText, "\n");
      console.log(`${diagnostic.file.fileName} (${line + 1},${character + 1}): ${message}`);
    } else {
      console.log(ts.flattenDiagnosticMessageText(diagnostic.messageText, "\n"));
    }
  });

  const exitCode = emitResult.emitSkipped ? 1 : 0;
  console.log(`Process exiting with code '${exitCode}'.`);
}

// Usage
compile(["src/app.ts", "src/utils.ts"], {
  noEmitOnError: true,
  noImplicitAny: true,
  target: ts.ScriptTarget.ES2020,
  module: ts.ModuleKind.CommonJS,
  outDir: "./dist"
});
```

## ts.transpileModule() - Simple String Transformation

Quickly transform TypeScript source code to JavaScript without creating a full Program.

```typescript
import * as ts from "typescript";

// Simple TypeScript to JavaScript transformation
const source = `
  interface User {
    name: string;
    age: number;
  }

  const greet = (user: User): string => {
    return \`Hello, \${user.name}! You are \${user.age} years old.\`;
  };

  export { greet, User };
`;

const result = ts.transpileModule(source, {
  compilerOptions: {
    module: ts.ModuleKind.CommonJS,
    target: ts.ScriptTarget.ES2015,
    removeComments: true,
    declaration: false
  },
  fileName: "example.ts"
});

console.log("Transpiled JavaScript:");
console.log(result.outputText);
// Output:
// "use strict";
// Object.defineProperty(exports, "__esModule", { value: true });
// exports.greet = void 0;
// const greet = (user) => {
//     return `Hello, ${user.name}! You are ${user.age} years old.`;
// };
// exports.greet = greet;

console.log("\nSource Map:");
console.log(result.sourceMapText);
```

## ts.createSourceFile() - Parse Source Code to AST

Parse TypeScript or JavaScript source code into an Abstract Syntax Tree (AST).

```typescript
import * as ts from "typescript";
import { readFileSync } from "fs";

// Create a SourceFile from source text
const sourceCode = `
function add(a: number, b: number): number {
  return a + b;
}

const result = add(1, 2);
console.log(result);
`;

const sourceFile = ts.createSourceFile(
  "example.ts",
  sourceCode,
  ts.ScriptTarget.ES2020,
  /* setParentNodes */ true,
  ts.ScriptKind.TS
);

// Traverse the AST
function visit(node: ts.Node, depth: number = 0): void {
  const indent = "  ".repeat(depth);
  console.log(`${indent}${ts.SyntaxKind[node.kind]}`);
  ts.forEachChild(node, child => visit(child, depth + 1));
}

console.log("AST Structure:");
visit(sourceFile);
// Output shows the tree structure:
// SourceFile
//   FunctionDeclaration
//     Identifier
//     Parameter
//       Identifier
//       NumberKeyword
//     ...
```

## ts.forEachChild() - Traverse AST Nodes

Walk through AST nodes to analyze or transform code.

```typescript
import * as ts from "typescript";
import { readFileSync } from "fs";

// Simple linter that checks coding style
function delint(sourceFile: ts.SourceFile): void {
  function delintNode(node: ts.Node): void {
    switch (node.kind) {
      // Check loop bodies are wrapped in blocks
      case ts.SyntaxKind.ForStatement:
      case ts.SyntaxKind.ForInStatement:
      case ts.SyntaxKind.WhileStatement:
      case ts.SyntaxKind.DoStatement:
        if ((node as ts.IterationStatement).statement.kind !== ts.SyntaxKind.Block) {
          report(node, "A looping statement's contents should be wrapped in a block body.");
        }
        break;

      // Check if statements use blocks
      case ts.SyntaxKind.IfStatement:
        const ifStatement = node as ts.IfStatement;
        if (ifStatement.thenStatement.kind !== ts.SyntaxKind.Block) {
          report(ifStatement.thenStatement, "An if statement's contents should be wrapped in a block body.");
        }
        break;

      // Check for strict equality operators
      case ts.SyntaxKind.BinaryExpression:
        const op = (node as ts.BinaryExpression).operatorToken.kind;
        if (op === ts.SyntaxKind.EqualsEqualsToken || op === ts.SyntaxKind.ExclamationEqualsToken) {
          report(node, "Use '===' and '!==' instead of '==' and '!='.");
        }
        break;
    }

    // Continue traversing child nodes
    ts.forEachChild(node, delintNode);
  }

  function report(node: ts.Node, message: string): void {
    const { line, character } = sourceFile.getLineAndCharacterOfPosition(node.getStart());
    console.log(`${sourceFile.fileName} (${line + 1},${character + 1}): ${message}`);
  }

  delintNode(sourceFile);
}

// Usage
const fileName = "example.ts";
const sourceFile = ts.createSourceFile(
  fileName,
  readFileSync(fileName).toString(),
  ts.ScriptTarget.ES2015,
  /* setParentNodes */ true
);

delint(sourceFile);
```

## TypeChecker - Type Analysis and Symbol Resolution

Use the TypeChecker to retrieve type information and symbols from the AST.

```typescript
import * as ts from "typescript";
import * as fs from "fs";

interface DocEntry {
  name?: string;
  documentation?: string;
  type?: string;
  constructors?: DocEntry[];
  parameters?: DocEntry[];
  returnType?: string;
}

function generateDocumentation(fileNames: string[], options: ts.CompilerOptions): DocEntry[] {
  const program = ts.createProgram(fileNames, options);
  const checker = program.getTypeChecker();
  const output: DocEntry[] = [];

  // Visit all source files
  for (const sourceFile of program.getSourceFiles()) {
    if (!sourceFile.isDeclarationFile) {
      ts.forEachChild(sourceFile, visit);
    }
  }

  return output;

  function visit(node: ts.Node): void {
    // Only consider exported nodes
    if (!isNodeExported(node)) return;

    if (ts.isClassDeclaration(node) && node.name) {
      const symbol = checker.getSymbolAtLocation(node.name);
      if (symbol) {
        output.push(serializeClass(symbol));
      }
    } else if (ts.isModuleDeclaration(node)) {
      ts.forEachChild(node, visit);
    }
  }

  function serializeSymbol(symbol: ts.Symbol): DocEntry {
    return {
      name: symbol.getName(),
      documentation: ts.displayPartsToString(symbol.getDocumentationComment(checker)),
      type: checker.typeToString(
        checker.getTypeOfSymbolAtLocation(symbol, symbol.valueDeclaration!)
      )
    };
  }

  function serializeClass(symbol: ts.Symbol): DocEntry {
    const details = serializeSymbol(symbol);
    const constructorType = checker.getTypeOfSymbolAtLocation(symbol, symbol.valueDeclaration!);
    details.constructors = constructorType.getConstructSignatures().map(serializeSignature);
    return details;
  }

  function serializeSignature(signature: ts.Signature): DocEntry {
    return {
      parameters: signature.parameters.map(serializeSymbol),
      returnType: checker.typeToString(signature.getReturnType()),
      documentation: ts.displayPartsToString(signature.getDocumentationComment(checker))
    };
  }

  function isNodeExported(node: ts.Node): boolean {
    return (
      (ts.getCombinedModifierFlags(node as ts.Declaration) & ts.ModifierFlags.Export) !== 0 ||
      (!!node.parent && node.parent.kind === ts.SyntaxKind.SourceFile)
    );
  }
}

// Usage
const docs = generateDocumentation(["src/models.ts"], {
  target: ts.ScriptTarget.ES5,
  module: ts.ModuleKind.CommonJS
});

console.log(JSON.stringify(docs, null, 2));
```

## ts.createPrinter() - Print AST to Source Code

Generate source code from AST nodes using the printer API.

```typescript
import * as ts from "typescript";

// Create a factorial function programmatically
function makeFactorialFunction(): ts.FunctionDeclaration {
  const functionName = ts.factory.createIdentifier("factorial");
  const paramName = ts.factory.createIdentifier("n");

  const parameter = ts.factory.createParameterDeclaration(
    undefined,           // modifiers
    undefined,           // dotDotDotToken
    paramName,
    undefined,           // questionToken
    ts.factory.createKeywordTypeNode(ts.SyntaxKind.NumberKeyword)
  );

  // if (n <= 1) { return 1; }
  const condition = ts.factory.createBinaryExpression(
    paramName,
    ts.SyntaxKind.LessThanEqualsToken,
    ts.factory.createNumericLiteral(1)
  );
  const ifBody = ts.factory.createBlock(
    [ts.factory.createReturnStatement(ts.factory.createNumericLiteral(1))],
    true
  );

  // return n * factorial(n - 1);
  const decrementedArg = ts.factory.createBinaryExpression(
    paramName,
    ts.SyntaxKind.MinusToken,
    ts.factory.createNumericLiteral(1)
  );
  const recurse = ts.factory.createBinaryExpression(
    paramName,
    ts.SyntaxKind.AsteriskToken,
    ts.factory.createCallExpression(functionName, undefined, [decrementedArg])
  );

  const statements = [
    ts.factory.createIfStatement(condition, ifBody),
    ts.factory.createReturnStatement(recurse)
  ];

  return ts.factory.createFunctionDeclaration(
    [ts.factory.createToken(ts.SyntaxKind.ExportKeyword)],
    undefined,           // asteriskToken
    functionName,
    undefined,           // typeParameters
    [parameter],
    ts.factory.createKeywordTypeNode(ts.SyntaxKind.NumberKeyword),
    ts.factory.createBlock(statements, true)
  );
}

// Create a source file and printer
const resultFile = ts.createSourceFile(
  "generated.ts",
  "",
  ts.ScriptTarget.Latest,
  false,
  ts.ScriptKind.TS
);

const printer = ts.createPrinter({ newLine: ts.NewLineKind.LineFeed });

// Print the generated function
const result = printer.printNode(
  ts.EmitHint.Unspecified,
  makeFactorialFunction(),
  resultFile
);

console.log(result);
// Output:
// export function factorial(n: number): number {
//     if (n <= 1) {
//         return 1;
//     }
//     return n * factorial(n - 1);
// }
```

## ts.createLanguageService() - Editor Integration

Create a Language Service for IDE-like features including completions, diagnostics, and quick fixes.

```typescript
import * as fs from "fs";
import * as ts from "typescript";

function createLanguageServiceDemo(rootFileNames: string[], options: ts.CompilerOptions) {
  const files: { [fileName: string]: { version: number } } = {};

  // Initialize file versions
  rootFileNames.forEach(fileName => {
    files[fileName] = { version: 0 };
  });

  // Create the Language Service Host
  const servicesHost: ts.LanguageServiceHost = {
    getScriptFileNames: () => rootFileNames,
    getScriptVersion: fileName => files[fileName]?.version.toString() || "0",
    getScriptSnapshot: fileName => {
      if (!fs.existsSync(fileName)) return undefined;
      return ts.ScriptSnapshot.fromString(fs.readFileSync(fileName, "utf8"));
    },
    getCurrentDirectory: () => process.cwd(),
    getCompilationSettings: () => options,
    getDefaultLibFileName: options => ts.getDefaultLibFilePath(options),
    fileExists: ts.sys.fileExists,
    readFile: ts.sys.readFile,
    readDirectory: ts.sys.readDirectory,
    directoryExists: ts.sys.directoryExists,
    getDirectories: ts.sys.getDirectories,
  };

  // Create the Language Service
  const services = ts.createLanguageService(servicesHost, ts.createDocumentRegistry());

  // Get diagnostics for a file
  function getDiagnostics(fileName: string): void {
    const syntactic = services.getSyntacticDiagnostics(fileName);
    const semantic = services.getSemanticDiagnostics(fileName);
    const suggestions = services.getSuggestionDiagnostics(fileName);

    [...syntactic, ...semantic, ...suggestions].forEach(diagnostic => {
      const message = ts.flattenDiagnosticMessageText(diagnostic.messageText, "\n");
      if (diagnostic.file) {
        const { line, character } = diagnostic.file.getLineAndCharacterOfPosition(diagnostic.start!);
        console.log(`${diagnostic.file.fileName} (${line + 1},${character + 1}): ${message}`);
      } else {
        console.log(`Error: ${message}`);
      }
    });
  }

  // Get completions at a position
  function getCompletions(fileName: string, position: number): void {
    const completions = services.getCompletionsAtPosition(fileName, position, undefined);
    if (completions) {
      console.log("Completions:", completions.entries.slice(0, 10).map(e => e.name));
    }
  }

  // Get quick info (hover) at a position
  function getQuickInfo(fileName: string, position: number): void {
    const info = services.getQuickInfoAtPosition(fileName, position);
    if (info) {
      console.log("Quick Info:", ts.displayPartsToString(info.displayParts));
      if (info.documentation) {
        console.log("Documentation:", ts.displayPartsToString(info.documentation));
      }
    }
  }

  return { services, getDiagnostics, getCompletions, getQuickInfo };
}

// Usage
const { getDiagnostics, getCompletions, getQuickInfo } = createLanguageServiceDemo(
  ["src/app.ts"],
  { module: ts.ModuleKind.CommonJS, target: ts.ScriptTarget.ES2020 }
);

getDiagnostics("src/app.ts");
getCompletions("src/app.ts", 50);  // Get completions at character position 50
getQuickInfo("src/app.ts", 25);    // Get hover info at character position 25
```

## ts.createWatchCompilerHost() - File Watching

Create a watch program for incremental compilation when files change.

```typescript
import * as ts from "typescript";

const formatHost: ts.FormatDiagnosticsHost = {
  getCanonicalFileName: path => path,
  getCurrentDirectory: ts.sys.getCurrentDirectory,
  getNewLine: () => ts.sys.newLine
};

function watchMain(): void {
  // Find tsconfig.json
  const configPath = ts.findConfigFile(
    "./",
    ts.sys.fileExists,
    "tsconfig.json"
  );

  if (!configPath) {
    throw new Error("Could not find a valid 'tsconfig.json'.");
  }

  // Create a semantic diagnostics builder program for incremental compilation
  const createProgram = ts.createSemanticDiagnosticsBuilderProgram;

  // Create the watch compiler host
  const host = ts.createWatchCompilerHost(
    configPath,
    {},
    ts.sys,
    createProgram,
    reportDiagnostic,
    reportWatchStatusChanged
  );

  // Hook into program creation for custom logic
  const origCreateProgram = host.createProgram;
  host.createProgram = (rootNames, options, host, oldProgram) => {
    console.log("** Starting compilation... **");
    return origCreateProgram(rootNames, options, host, oldProgram);
  };

  const origPostProgramCreate = host.afterProgramCreate;
  host.afterProgramCreate = program => {
    console.log("** Compilation finished! **");
    origPostProgramCreate!(program);
  };

  // Start watching
  ts.createWatchProgram(host);
}

function reportDiagnostic(diagnostic: ts.Diagnostic): void {
  console.error(
    "Error",
    diagnostic.code,
    ":",
    ts.flattenDiagnosticMessageText(diagnostic.messageText, formatHost.getNewLine())
  );
}

function reportWatchStatusChanged(diagnostic: ts.Diagnostic): void {
  console.info(ts.formatDiagnostic(diagnostic, formatHost));
}

// Start the watcher
watchMain();
```

## ts.createCompilerHost() - Custom File Resolution

Create a custom CompilerHost to control how the compiler reads and resolves files.

```typescript
import * as ts from "typescript";
import * as path from "path";

function createCustomCompilerHost(
  options: ts.CompilerOptions,
  moduleSearchLocations: string[]
): ts.CompilerHost {
  return {
    getSourceFile,
    getDefaultLibFileName: () => "lib.d.ts",
    writeFile: (fileName, content) => ts.sys.writeFile(fileName, content),
    getCurrentDirectory: () => ts.sys.getCurrentDirectory(),
    getDirectories: path => ts.sys.getDirectories(path),
    getCanonicalFileName: fileName =>
      ts.sys.useCaseSensitiveFileNames ? fileName : fileName.toLowerCase(),
    getNewLine: () => ts.sys.newLine,
    useCaseSensitiveFileNames: () => ts.sys.useCaseSensitiveFileNames,
    fileExists,
    readFile,
    resolveModuleNames
  };

  function fileExists(fileName: string): boolean {
    return ts.sys.fileExists(fileName);
  }

  function readFile(fileName: string): string | undefined {
    return ts.sys.readFile(fileName);
  }

  function getSourceFile(
    fileName: string,
    languageVersion: ts.ScriptTarget,
    onError?: (message: string) => void
  ): ts.SourceFile | undefined {
    const sourceText = ts.sys.readFile(fileName);
    return sourceText !== undefined
      ? ts.createSourceFile(fileName, sourceText, languageVersion)
      : undefined;
  }

  function resolveModuleNames(
    moduleNames: string[],
    containingFile: string
  ): (ts.ResolvedModule | undefined)[] {
    const resolvedModules: (ts.ResolvedModule | undefined)[] = [];

    for (const moduleName of moduleNames) {
      // Try standard resolution first
      const result = ts.resolveModuleName(moduleName, containingFile, options, {
        fileExists,
        readFile
      });

      if (result.resolvedModule) {
        resolvedModules.push(result.resolvedModule);
      } else {
        // Check custom fallback locations
        let found = false;
        for (const location of moduleSearchLocations) {
          const modulePath = path.join(location, moduleName + ".d.ts");
          if (fileExists(modulePath)) {
            resolvedModules.push({ resolvedFileName: modulePath });
            found = true;
            break;
          }
        }
        if (!found) {
          resolvedModules.push(undefined);
        }
      }
    }

    return resolvedModules;
  }
}

// Usage
const options: ts.CompilerOptions = {
  module: ts.ModuleKind.CommonJS,
  target: ts.ScriptTarget.ES2020
};

const host = createCustomCompilerHost(options, ["./custom-types", "./vendor-types"]);
const program = ts.createProgram(["src/app.ts"], options, host);

// Emit with custom host
program.emit();
```

## Declaration File Generation

Generate `.d.ts` declaration files from JavaScript files with JSDoc annotations.

```typescript
import * as ts from "typescript";

function generateDeclarations(fileNames: string[]): void {
  const options: ts.CompilerOptions = {
    allowJs: true,
    declaration: true,
    emitDeclarationOnly: true,
    outDir: "./types"
  };

  // Create in-memory emit to capture output
  const createdFiles: { [fileName: string]: string } = {};
  const host = ts.createCompilerHost(options);

  host.writeFile = (fileName, contents) => {
    createdFiles[fileName] = contents;
  };

  const program = ts.createProgram(fileNames, options, host);
  program.emit();

  // Display generated declarations
  for (const [fileName, content] of Object.entries(createdFiles)) {
    console.log(`=== ${fileName} ===`);
    console.log(content);
  }
}

// Example JavaScript file with JSDoc (math.js):
// /**
//  * Adds two numbers together
//  * @param {number} a - First number
//  * @param {number} b - Second number
//  * @returns {number} The sum
//  */
// export function add(a, b) {
//   return a + b;
// }

generateDeclarations(["src/math.js"]);
// Output: types/math.d.ts
// export function add(a: number, b: number): number;
```

## Summary

TypeScript's Compiler API provides comprehensive programmatic access to all phases of compilation. The core APIs include `createProgram()` for building compilation contexts, `createSourceFile()` for parsing code into ASTs, `forEachChild()` for traversing syntax trees, `TypeChecker` for semantic analysis and type resolution, and `createPrinter()` for code generation. These APIs enable building sophisticated tooling that leverages TypeScript's static analysis capabilities.

The Language Service API extends this functionality for editor integrations, providing completions, diagnostics, refactoring suggestions, and symbol navigation. The watch APIs enable incremental compilation for development workflows. Common use cases include building custom linters, documentation generators, code transformers, IDE plugins, build tool integrations, and static analysis tools. The API's flexibility in customizing module resolution and file handling makes it suitable for integration into diverse development environments and toolchains.
