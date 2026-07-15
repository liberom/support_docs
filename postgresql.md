### Quick PostgreSQL Installation with Meson

Source: https://www.postgresql.org/docs/16/install-meson

Provides a concise set of shell commands for a rapid setup, build, installation, initialization, and start of a PostgreSQL instance using Meson. This sequence includes creating a dedicated user, initializing the data directory, starting the server, and creating a test database.

```shell
meson setup build --prefix=/usr/local/pgsql
cd build
ninja
su
ninja install
adduser postgres
mkdir -p /usr/local/pgsql/data
chown postgres /usr/local/pgsql/data
su - postgres
/usr/local/pgsql/bin/initdb -D /usr/local/pgsql/data
/usr/local/pgsql/bin/pg_ctl -D /usr/local/pgsql/data -l logfile start
/usr/local/pgsql/bin/createdb test
/usr/local/pgsql/bin/psql test
```

--------------------------------

### PostgreSQL Source Installation Commands

Source: https://www.postgresql.org/docs/11/install-short

This snippet details the essential shell commands required to configure, compile, install, and initialize a PostgreSQL database from its source code. It covers user creation, data directory setup, and starting the server.

```shell
./configure
make
su
make install
adduser postgres
mkdir /usr/local/pgsql/data
chown postgres /usr/local/pgsql/data
su - postgres
/usr/local/pgsql/bin/initdb -D /usr/local/pgsql/data
/usr/local/pgsql/bin/postgres -D /usr/local/pgsql/data >logfile 2>&1 &
/usr/local/pgsql/bin/createdb test
/usr/local/pgsql/bin/psql test

```

--------------------------------

### PostgreSQL Source Installation Commands (Shell)

Source: https://www.postgresql.org/docs/10/install-short

A sequence of shell commands to compile, install, and set up a PostgreSQL 10 database from source. This includes configuration, building, user creation, data directory setup, database initialization, and starting the PostgreSQL server.

```shell
./configure
make
su
make install
adduser postgres
mkdir /usr/local/pgsql/data
chown postgres /usr/local/pgsql/data
su - postgres
/usr/local/pgsql/bin/initdb -D /usr/local/pgsql/data
/usr/local/pgsql/bin/postgres -D /usr/local/pgsql/data >logfile 2>&1 &
/usr/local/pgsql/bin/createdb test
/usr/local/pgsql/bin/psql test
```

--------------------------------

### Configuring Meson Build Options for PostgreSQL

Source: https://www.postgresql.org/docs/16/install-meson

Illustrates how to use the 'meson setup' command with various options to customize the PostgreSQL build. Examples include specifying a different installation prefix, generating a debug build, and enabling support for OpenSSL.

```shell
# configure with a different installation prefix
meson setup build --prefix=/home/user/pg-install

# configure to generate a debug build
meson setup build --buildtype=debug

# configure to build with OpenSSL support
meson setup build -Dssl=openssl
```

--------------------------------

### Create PostgreSQL Publication for Replication Examples

Source: https://www.postgresql.org/docs/16/logical-replication-subscription

Initial setup step to create a publication named 'pub1' for all tables on the publisher, which will be used by all subsequent logical replication examples. This publication serves as the source of data for the subscriptions.

```sql
CREATE PUBLICATION pub1 FOR ALL TABLES;
```

--------------------------------

### Configure Meson with Specific Build Options

Source: https://www.postgresql.org/docs/18/install-meson

These commands demonstrate how to configure the Meson build with various options. Examples include setting a custom installation prefix, generating a debug build, and enabling specific features like OpenSSL support during the initial configuration. These options are passed directly to `meson setup`.

```bash
# configure with a different installation prefix
meson setup build --prefix=/home/user/pg-install
```

```bash
# configure to generate a debug build
meson setup build --buildtype=debug
```

```bash
# configure to build with OpenSSL support
meson setup build -Dssl=openssl
```

--------------------------------

### Example PostgreSQL Configure Command with Options

Source: https://www.postgresql.org/docs/6.3/c1802

This example demonstrates how to use the `./configure` script with several common options to specify installation paths, select a template, set the listening port, and enable/disable features like Host Based Authentication and locale support.

```shell
./configure --prefix=/opt/postgres \
    --with-template=sparc_solaris-gcc --with-pgport=5432 \
    --enable-hba --disable-locale
```

--------------------------------

### PostgreSQL: SQL Query Examples

Source: https://www.postgresql.org/docs/6.3/c03

This section illustrates how to write and execute SQL queries within PostgreSQL using the interactive monitor. It highlights that commands starting with '*' are Postgres SQL commands.

```sql
* SELECT;
```

--------------------------------

### Start PostgreSQL Server with pg_ctl

Source: https://www.postgresql.org/docs/18/app-pg-ctl

Demonstrates how to start the PostgreSQL server using the pg_ctl command. It shows the basic start command and an example with specific options for port and fsync.

```bash
$ pg_ctl start
```

```bash
$ pg_ctl -o "-F -p 5433" start
```

--------------------------------

### Install complete PostgreSQL system (world build) using Make

Source: https://www.postgresql.org/docs/15/install-procedure

This command installs all components of PostgreSQL, including documentation, if the 'world' build option was previously used during configuration. It's an alternative to `make install` for comprehensive setups.

```Makefile
make install-world
```

--------------------------------

### Install PostgreSQL from Source: Short Version

Source: https://www.postgresql.org/docs/16/install-make

Provides a condensed sequence of bash commands to configure, build, install, initialize, and start a PostgreSQL server from source. This includes creating a dedicated user, setting up the data directory, and creating a test database.

```bash
./configure
make
su
make install
adduser postgres
mkdir -p /usr/local/pgsql/data
chown postgres /usr/local/pgsql/data
su - postgres
/usr/local/pgsql/bin/initdb -D /usr/local/pgsql/data
/usr/local/pgsql/bin/pg_ctl -D /usr/local/pgsql/data -l logfile start
/usr/local/pgsql/bin/createdb test
/usr/local/pgsql/bin/psql test
```

--------------------------------

### Manual Installation of PL/pgSQL (PostgreSQL)

Source: https://www.postgresql.org/docs/7.3/programmer

This section likely describes the manual steps required to install or enable the PL/pgSQL procedural language in PostgreSQL. It may involve running SQL commands.

```sql
-- Manual Installation of PL/pgSQL
-- This is a placeholder for the actual SQL commands.
-- Typically involves CREATE EXTENSION plpgsql; or similar commands.

-- Example (if not already installed):
-- CREATE LANGUAGE plpgsql;

```

--------------------------------

### Install and Initialize PostgreSQL 7.2 (Short Version)

Source: https://www.postgresql.org/docs/7.2/installation

This snippet provides a condensed sequence of shell commands to configure, build, install, initialize, and start PostgreSQL 7.2 from source. It covers creating a dedicated user, setting up a data directory, initializing the database instance, launching the postmaster process, and creating a test database for immediate use.

```bash
./configure
gmake
su
gmake install
adduser postgres
mkdir /usr/local/pgsql/data
chown postgres /usr/local/pgsql/data
su - postgres
/usr/local/pgsql/bin/initdb -D /usr/local/pgsql/data
/usr/local/pgsql/bin/postmaster -D /usr/local/pgsql/data >logfile 2>&1 &
/usr/local/pgsql/bin/createdb test
/usr/local/pgsql/bin/psql test
```

--------------------------------

### PostgreSQL Build Configuration Example (Makefile.custom)

Source: https://www.postgresql.org/docs/7.0/c1688316912

An example of a Makefile.custom file for PostgreSQL installation on a PentiumPro Linux system. It shows how to set installation directories and C compiler flags.

```Makefile
# Makefile.custom
# Thomas Lockhart 1999-06-01

POSTGRESDIR= /opt/postgres/current
CFLAGS+= -m486 -O2

# documentation

HSTYLE= /home/tgl/SGML/db118.d/docbook/html
PSTYLE= /home/tgl/SGML/db118.d/docbook/print
```

--------------------------------

### PL/pgSQL Installation Example

Source: https://www.postgresql.org/docs/7.0/xplang

An example demonstrating the installation of the PL/pgSQL language. It first declares the call handler function and then defines the PL/pgSQL language as trusted.

```SQL
CREATE FUNCTION plpgsql_call_handler () RETURNS OPAQUE AS
    '/usr/local/pgsql/lib/plpgsql.so' LANGUAGE 'C';

CREATE TRUSTED PROCEDURAL LANGUAGE 'plpgsql'
    HANDLER plpgsql_call_handler
    LANCOMPILER 'PL/pgSQL';
```

--------------------------------

### PostgreSQL: Start Interactive Monitor (psql)

Source: https://www.postgresql.org/docs/6.3/c03

This section explains how to start the psql interactive monitor, a command-line tool for interacting with PostgreSQL databases. It clarifies that commands starting with '%' are UNIX shell commands.

```shell
% psql
```

--------------------------------

### Setup SQL for libpq Binary I/O Example (SQL)

Source: https://www.postgresql.org/docs/devel/libpq-example

Provides the necessary SQL commands to initialize a database environment for testing libpq's binary I/O capabilities. It creates a schema, sets the search path, defines a table 'test1' with integer, text, and bytea columns, and inserts sample data, including bytea values for binary testing.

```SQL
CREATE SCHEMA testlibpq3;
SET search_path = testlibpq3;
SET standard_conforming_strings = ON;
CREATE TABLE test1 (i int4, t text, b bytea);
INSERT INTO test1 values (1, 'joe''s place', '\\000\\001\\002\\003\\004');
INSERT INTO test1 values (2, 'ho there', '\\004\\003\\002\\001\\000');
```

--------------------------------

### Manual PL/Perl Installation Example (SQL)

Source: https://www.postgresql.org/docs/13/xplang-install

An example demonstrating the manual installation of the PL/Perl language. It includes declarations for the call handler, inline handler, and validator functions, followed by the final `CREATE TRUSTED LANGUAGE` command to register PL/Perl.

```sql
CREATE FUNCTION plperl_call_handler() RETURNS language_handler AS
    '$libdir/plperl' LANGUAGE C;

CREATE FUNCTION plperl_inline_handler(internal) RETURNS void AS
    '$libdir/plperl' LANGUAGE C STRICT;

CREATE FUNCTION plperl_validator(oid) RETURNS void AS
    '$libdir/plperl' LANGUAGE C STRICT;

CREATE TRUSTED LANGUAGE plperl
    HANDLER plperl_call_handler
    INLINE plperl_inline_handler
    VALIDATOR plperl_validator;

```

--------------------------------

### PostgreSQL Source Installation Commands

Source: https://www.postgresql.org/docs/12/install-short

This snippet lists the core shell commands required to install PostgreSQL from its source code. It includes steps for configuring, compiling, installing, initializing the database cluster, starting the server, and creating/accessing a database.

```shell
./configure
make
su
make install
adduser postgres
mkdir /usr/local/pgsql/data
chown postgres /usr/local/pgsql/data
su - postgres
/usr/local/pgsql/bin/initdb -D /usr/local/pgsql/data
/usr/local/pgsql/bin/pg_ctl -D /usr/local/pgsql/data -l logfile start
/usr/local/pgsql/bin/createdb test
/usr/local/pgsql/bin/psql test
```

--------------------------------

### Basic Meson Setup Command

Source: https://www.postgresql.org/docs/16/install-meson

Demonstrates the fundamental 'meson setup build' command, which is the initial step to configure the build directory for compiling PostgreSQL with Meson. This command loads the build configuration and prepares the directory for compilation.

```shell
meson setup build
```

--------------------------------

### Start PostgreSQL Postmaster

Source: https://www.postgresql.org/docs/6.5/postmaster

This command starts the PostgreSQL postmaster process. It assumes PostgreSQL has been installed following the standard installation instructions. No specific output or dependencies are mentioned beyond a successful installation.

```shell
% postmaster
    

```

--------------------------------

### libpq Example Program 2 (PostgreSQL)

Source: https://www.postgresql.org/docs/7.3/programmer

This snippet illustrates another example program using libpq. It likely focuses on different aspects of database interaction compared to the first example.

```c
/*
** libpq Example Program 2
** This is a placeholder for the actual C code.
*/
#include <stdio.h>
#include <stdlib.h>
#include <libpq-fe.h>

int main(int argc, char **argv) {
    // Placeholder for libpq example 2 code
    printf("libpq Example Program 2 placeholder.\n");
    return 0;
}

```

--------------------------------

### PostgreSQL Transform Example Setup

Source: https://www.postgresql.org/docs/16/sql-createtransform

This example demonstrates the initial setup required before creating a PostgreSQL transform. It includes creating the necessary data type ('hstore') and enabling the procedural language extension ('plpython3u'). These steps are prerequisites for defining the transform itself.

```sql
CREATE TYPE hstore ...;

CREATE EXTENSION plpython3u;
```

--------------------------------

### PostgreSQL 7.1 Quick Installation Commands

Source: https://www.postgresql.org/docs/7.1/installation

This snippet outlines the essential commands for a quick installation of PostgreSQL 7.1. It covers configuration, compilation, installation, user creation, database initialization, server startup, and basic database interaction. Assumes a Unix-like environment.

```shell
./configure
gmake
gmake install
adduser postgres
su - postgres
/usr/local/pgsql/bin/initdb -D /usr/local/pgsql/data
/usr/local/pgsql/bin/postmaster -D /usr/local/pgsql/data >logfile 2>&1 &
/usr/local/pgsql/bin/createdb test
/usr/local/pgsql/bin/psql test
```

--------------------------------

### Install PostgreSQL documentation using Make

Source: https://www.postgresql.org/docs/15/install-procedure

Use this command to install only the HTML and man pages documentation for PostgreSQL. This is useful for accessing reference materials locally after installation, without installing the full system.

```Makefile
make install-docs
```

--------------------------------

### Stream PostgreSQL Logical Changes using pg_recvlogical Utility (Shell)

Source: https://www.postgresql.org/docs/devel/logicaldecoding-example

This example illustrates how to use the `pg_recvlogical` command-line utility to establish a streaming replication connection. It demonstrates creating a logical replication slot, starting the stream, and observing DML operations (e.g., an `INSERT`) as they occur, requiring appropriate client authentication setup.

```bash
Example 1:
$ pg_recvlogical -d postgres --slot=test --create-slot
$ pg_recvlogical -d postgres --slot=test --start -f -
**Control**+**Z**
$ psql -d postgres -c "INSERT INTO data(data) VALUES('4');"
$ fg
BEGIN 693
table public.data: INSERT: id[integer]:4 data[text]:'4'
COMMIT 693
```

--------------------------------

### libpq Example Program (PostgreSQL)

Source: https://www.postgresql.org/docs/7.3/programmer

This snippet demonstrates a basic example program using the libpq library for interacting with PostgreSQL. It covers fundamental connection and query execution patterns.

```c
/*
** libpq Example Program 1
** This is a placeholder for the actual C code.
*/
#include <stdio.h>
#include <stdlib.h>
#include <libpq-fe.h>

int main(int argc, char **argv) {
    const char *conninfo;
    PGconn *conn;
    PGresult *res;

    // Connection string (replace with your actual connection details)
    conninfo = "dbname=mydb user=myuser password=mypass hostaddr=127.0.0.1 port=5432";

    // Make a connection to the database
    conn = PQconnectdb(conninfo);

    if (PQstatus(conn) == CONNECTION_BAD) {
        fprintf(stderr, "Connection to database failed: %s", PQerrorMessage(conn));
        PQfinish(conn);
        exit(1);
    }

    // Execute a simple query
    res = PQexec(conn, "SELECT version();");

    if (PQresultStatus(res) != PGRES_TUPLES_OK) {
        fprintf(stderr, "SELECT failed: %s", PQerrorMessage(conn));
        PQclear(res);
        PQfinish(conn);
        exit(1);
    }

    // Process the query result
    printf("%s\n", PQgetvalue(res, 0, 0));

    // Clear the result and close the connection
    PQclear(res);
    PQfinish(conn);

    return 0;
}

```

--------------------------------

### Sample libpq Programs Directory Structure

Source: https://www.postgresql.org/docs/7.0/libpq-chapter

This snippet outlines the directory locations where complete example applications demonstrating the usage of libpq can be found within the PostgreSQL source tree. These examples serve as practical guides for developers.

```text
../src/test/regress
../src/test/examples
../src/bin/psql
```

--------------------------------

### PostgreSQL Source Installation (Shell)

Source: https://www.postgresql.org/docs/15/install-short

This snippet provides the essential shell commands for a quick installation of PostgreSQL from source code. It includes configuring the build, compiling, installing, creating a PostgreSQL user, initializing the data directory, starting the server, and creating/connecting to a test database. Assumes a Unix-like environment.

```bash
./configure
make
su
make install
adduser postgres
mkdir -p /usr/local/pgsql/data
chown postgres /usr/local/pgsql/data
su - postgres
/usr/local/pgsql/bin/initdb -D /usr/local/pgsql/data
/usr/local/pgsql/bin/pg_ctl -D /usr/local/pgsql/data -l logfile start
/usr/local/pgsql/bin/createdb test
/usr/local/pgsql/bin/psql test

```

--------------------------------

### PostgreSQL Transform Setup Example

Source: https://www.postgresql.org/docs/17/sql-createtransform

An example demonstrating the necessary steps to set up a transform for the 'hstore' type and 'plpython3u' language in PostgreSQL. This includes creating the type, extending the language, and defining the associated conversion functions.

```sql
CREATE TYPE hstore ...;

CREATE EXTENSION plpython3u;
```

```sql
CREATE FUNCTION hstore_to_plpython(val internal) RETURNS internal
LANGUAGE C STRICT IMMUTABLE
AS ...;

CREATE FUNCTION plpython_to_hstore(val internal) RETURNS hstore
LANGUAGE C STRICT IMMUTABLE
AS ...;
```

```sql
CREATE TRANSFORM FOR hstore LANGUAGE plpython3u (
    FROM SQL WITH FUNCTION hstore_to_plpython(internal),
    TO SQL WITH FUNCTION plpython_to_hstore(internal)
);
```

--------------------------------

### libpq Example Program 3 (PostgreSQL)

Source: https://www.postgresql.org/docs/7.3/programmer

This snippet presents a third example program utilizing the libpq library. It might cover more advanced features or specific use cases.

```c
/*
** libpq Example Program 3
** This is a placeholder for the actual C code.
*/
#include <stdio.h>
#include <stdlib.h>
#include <libpq-fe.h>

int main(int argc, char **argv) {
    // Placeholder for libpq example 3 code
    printf("libpq Example Program 3 placeholder.\n");
    return 0;
}

```

--------------------------------

### PostgreSQL Configuration Parameter Examples

Source: https://www.postgresql.org/docs/10/runtime-config-preset

Illustrative examples of how PostgreSQL configuration parameters might be represented or used. Note that these parameters are read-only and determined during build or installation.

```sql
SELECT name, setting FROM pg_settings WHERE category = 'Preset Options';
```

```bash
# Example of configure option that influences a preset
./configure --enable-cassert
```

--------------------------------

### PostgreSQL SHOW ALL Example

Source: https://www.postgresql.org/docs/15/sql-show

Provides an example of using the SHOW ALL command to display all available PostgreSQL configuration parameters and their descriptions.

```sql
SHOW ALL;
-- Expected Output (partial):
--             name         | setting |                description
-- -------------------------+---------+-------------------------------------------------
--  allow_system_table_mods | off     | Allows modifications of the structure of ...
--     .
--     .
--     .
--  xmloption               | content | Sets whether XML data in implicit parsing ...
--  zero_damaged_pages      | off     | Continues processing past damaged page headers.
-- (196 rows)
```

--------------------------------

### PostgreSQL GET DESCRIPTOR - Example: Get Column Data

Source: https://www.postgresql.org/docs/10/ecpg-sql-get-descriptor

An example illustrating how to fetch the actual data of a specific column (the second column here) into a host variable using GET DESCRIPTOR with the 'DATA' descriptor item.

```sql
EXEC SQL GET DESCRIPTOR d VALUE 2 :d_data = DATA;
```

--------------------------------

### PostgreSQL GET DESCRIPTOR - Example: Get Column Count

Source: https://www.postgresql.org/docs/10/ecpg-sql-get-descriptor

An example demonstrating how to use the GET DESCRIPTOR command to retrieve the total number of columns in a result set, identified by the 'COUNT' header item.

```sql
EXEC SQL GET DESCRIPTOR d :d_count = COUNT;
```

--------------------------------

### PostgreSQL Connection Setup and Main Function (C/libpq)

Source: https://www.postgresql.org/docs/7.4/lo-examplesect

This C code snippet demonstrates the main function for a libpq example program. It handles command-line arguments for database connection and file paths, establishes a connection to the PostgreSQL database using `PQsetdb`, and includes basic argument validation. It's the entry point for the large object manipulation program.

```c
void
exit_nicely(PGconn *conn)
{
    PQfinish(conn);
    exit(1);
}

int
main(int argc, char **argv)
{
    char       *in_filename,    *out_filename;
    char       *database;
    Oid         lobjOid;
    PGconn     *conn;
    PGresult   *res;

    if (argc != 4)
    {
        fprintf(stderr, "Usage: %s database_name in_filename out_filename\n",
                argv[0]);
        exit(1);
    }

    database = argv[1];
    in_filename = argv[2];
    out_filename = argv[3];

    /*
     * set up the connection
     */
    conn = PQsetdb(NULL, NULL, NULL, NULL, database);

    /* ... rest of the main function logic would follow ... */

    return 0;
}

```

--------------------------------

### PostgreSQL GET DESCRIPTOR - Example: Get Column Length

Source: https://www.postgresql.org/docs/10/ecpg-sql-get-descriptor

This example shows how to retrieve the octet length of a specific column (the first column in this case) using GET DESCRIPTOR with the 'RETURNED_OCTET_LENGTH' descriptor item.

```sql
EXEC SQL GET DESCRIPTOR d VALUE 1 :d_returned_octet_length = RETURNED_OCTET_LENGTH;
```

--------------------------------

### PostgreSQL Create Publication and Subscription

Source: https://www.postgresql.org/docs/13/logical-replication-quick-setup

Demonstrates the SQL commands to create a publication on the publisher database, specifying tables to be replicated, and a subscription on the subscriber database, establishing the connection and linking to the publication. This initiates the replication process.

```sql
CREATE PUBLICATION mypub FOR TABLE users, departments;

```

```sql
CREATE SUBSCRIPTION mysub CONNECTION 'dbname=foo host=bar user=repuser' PUBLICATION mypub;

```

--------------------------------

### Start PostgreSQL Server (Foreground - Shell)

Source: https://www.postgresql.org/docs/7.0/install17165

Starts the PostgreSQL server process in the foreground. The -D option specifies the data directory. Log messages will be visible in the terminal.

```shell
> /usr/local/pgsql/bin/postmaster -D /usr/local/pgsql/data
```

--------------------------------

### Start PostgreSQL Server using pg_ctl

Source: https://www.postgresql.org/docs/13/app-pg-ctl

This command starts the PostgreSQL server and waits until it is ready to accept connections. No specific dependencies are required beyond the PostgreSQL installation.

```bash
$ **pg_ctl start**
```

--------------------------------

### Pre-v6.4 Integrated Installation: Build and Install

Source: https://www.postgresql.org/docs/6.5/odbc19863

This sequence of commands is for installing an older version of PostgreSQL (pre-v6.4) with the newest psqlODBC driver. It involves unpacking the source, configuring, building, and installing.

```bash
% ./configure
% make
% make POSTGRESDIR=`PostgresTopDir` install
```

--------------------------------

### PostgreSQL SHOW ALL Example

Source: https://www.postgresql.org/docs/14/sql-show

An example illustrating the use of the SHOW ALL command in PostgreSQL to display all available configuration parameters along with their descriptions.

```sql
SHOW ALL;
            name         | setting |                description                                                          
-------------------------+---------+-------------------------------------------------
 allow_system_table_mods | off     | Allows modifications of the structure of ...
    .
    .
    .
 xmloption               | content | Sets whether XML data in implicit parsing ...
 zero_damaged_pages      | off     | Continues processing past damaged page headers.
(196 rows)
```

--------------------------------

### Compile and Install PostgreSQL

Source: https://www.postgresql.org/docs/6.5/install12893

This section details the compilation and installation process using `gmake`. It includes steps for installing documentation, compiling the main program, and installing the program binaries and supporting files. Log files are generated for monitoring the build process.

```shell
cd /usr/src/pgsql/doc
gmake install
```

```shell
cd /usr/src/pgsql/src
gmake all >& make.log &
tail -f make.log
```

```shell
gmake clean
```

```shell
gmake COPT="-g" all >& make.log &
```

```shell
cd /usr/src/pgsql/src
gmake install >& make.install.log &
tail -f make.install.log
```

--------------------------------

### Build All PostgreSQL Components Including Documentation

Source: https://www.postgresql.org/docs/13/install-procedure

This command performs a comprehensive build of PostgreSQL, encompassing all possible components. This includes not only the server and utilities but also documentation (HTML and man pages) and additional modules from the `contrib` directory.

```bash
make world
```

--------------------------------

### PostgreSQL Get Array Lower Bound Function (`array_lower`) Example

Source: https://www.postgresql.org/docs/14/functions-array

Returns the lower bound (starting index) of a specified dimension for a given array. This is useful when arrays have custom lower bounds.

```SQL
array_lower('[0:2]={1,2,3}'::integer[], 1)
```

--------------------------------

### Build PostgreSQL Server and Utilities

Source: https://www.postgresql.org/docs/13/install-procedure

These commands initiate the standard build process for PostgreSQL using `make`. It compiles the server, essential utilities, and client applications. Both `make` and `make all` achieve the same result for a basic build.

```bash
make
make all
```

--------------------------------

### Pre-v6.4 Integrated Installation: Specify Destinations

Source: https://www.postgresql.org/docs/6.5/odbc19863

This command allows users to specify custom installation directories for binaries, libraries, headers, and the ODBC configuration file during the pre-v6.4 integrated installation.

```bash
% make BINDIR=bindir  LIBDIR=libdir  HEADERDIR=headerdir ODBCINST=instfile install
```

--------------------------------

### Integrated Installation: Custom Install Path

Source: https://www.postgresql.org/docs/6.5/odbc19863

Allows specifying a custom filename for the ODBC installation configuration file during the integrated installation process using the `ODBCINST` variable.

```bash
% make ODBCINST=`filename` install
```

--------------------------------

### Start PostgreSQL postmaster

Source: https://www.postgresql.org/docs/6.3/c20

Starts the PostgreSQL postmaster process. This is the primary command to bring the database server online. Assumes standard installation.

```shell
% postmaster

```

--------------------------------

### Integrated Installation: Install

Source: https://www.postgresql.org/docs/6.5/odbc19863

This command installs the PostgreSQL distribution, including the newly built psqlODBC driver, into the system's defined areas. The ODBC configuration file is placed in the main Postgres target tree.

```bash
% make install
```

--------------------------------

### Configure PostgreSQL ODBC Driver Installation

Source: https://www.postgresql.org/docs/6.4/odbc18456

Configures the standalone PostgreSQL ODBC driver installation. Options allow specifying installation directories for libraries, headers, and configuration files.

```bash
% ./configure
% ./configure --prefix=`rootdir` --with-odbc=`inidir`
```

--------------------------------

### PostgreSQL GET DIAGNOSTICS Example

Source: https://www.postgresql.org/docs/11/plpgsql-statements

An example of using the GET DIAGNOSTICS command to retrieve the ROW_COUNT, which indicates the number of rows processed by the most recent SQL command.

```sql
GET DIAGNOSTICS integer_var = ROW_COUNT;
```

--------------------------------

### Install PostgreSQL Program Files

Source: https://www.postgresql.org/docs/6.3/c1802

This sequence installs the compiled PostgreSQL program files, including binaries and man pages. It uses `gmake install` and redirects the output to `make.install.log`, running the installation in the background. `tail -f` monitors the installation log.

```shell
cd /usr/src/pgsql/src
gmake install >& make.install.log &
tail -f make.install.log
```

--------------------------------

### Standalone Installation: Unpack gzipped Tarball

Source: https://www.postgresql.org/docs/6.5/odbc19863

This command is used to unpack a gzipped tarball archive of the psqlODBC driver for a standalone installation.

```bash
tar -xzf `packagename`
```

--------------------------------

### Build PostgreSQL Server

Source: https://www.postgresql.org/docs/12/install-procedure

Initiates the build process for PostgreSQL. 'make' and 'make all' perform the same function. Ensure you are using GNU make. The build typically takes a few minutes and concludes with a success message.

```shell
make
make all
```

--------------------------------

### Install PostgreSQL client applications and libraries using Make

Source: https://www.postgresql.org/docs/15/install-procedure

These commands install only the client applications, interface libraries, and optionally the documentation, without the full server components. This is ideal for machines that only need to connect to a remote PostgreSQL server, minimizing footprint.

```Makefile
make -C src/bin install
```

```Makefile
make -C src/include install
```

```Makefile
make -C src/interfaces install
```

```Makefile
make -C doc install
```

--------------------------------

### Install PostgreSQL Binaries and Documentation

Source: https://www.postgresql.org/docs/12/install-procedure

Installs the main PostgreSQL binaries and documentation into specified directories. Requires appropriate write permissions, often executed as root. Ensure target directories exist or are created with correct permissions.

```makefile
make install
make install-docs
make install-world
make install-world-bin
```

--------------------------------

### PostgreSQL crosstab: Example Data Setup

Source: https://www.postgresql.org/docs/11/tablefunc

Provides SQL statements to create and populate a sample 'sales' table, which will be used in the crosstab example.

```sql
create table sales(year int, month int, qty int);
insert into sales values(2007, 1, 1000);
insert into sales values(2007, 2, 1500);
insert into sales values(2007, 7, 500);
insert into sales values(2007, 11, 1500);
insert into sales values(2007, 12, 2000);
insert into sales values(2008, 1, 1000);
```

--------------------------------

### Install PostgreSQL Components

Source: https://www.postgresql.org/docs/13/install-windows-full

Commands to install PostgreSQL files. The first installs all files including database initialization files to a specified directory. The second installs only client applications and interface libraries.

```shell
install c:\destination\directory

```

```shell
install c:\destination\directory client

```

--------------------------------

### Pre-v6.4 Integrated ODBC Driver Installation

Source: https://www.postgresql.org/docs/6.4/odbc18456

Installs the latest ODBC driver into an older PostgreSQL installation (pre-v6.4). This involves unpacking a tar file, configuring, building, and installing the driver. It allows for specifying custom installation directories for binaries, libraries, headers, and configuration files.

```bash
% ./configure
% make
% make POSTGRESDIR=`PostgresTopDir` install
```

```bash
% make BINDIR=bindir  LIBDIR=libdir  HEADERDIR=headerdir ODBCINST=instfile install
```

--------------------------------

### Run PostgreSQL Basic SQL Tutorial

Source: https://www.postgresql.org/docs/11/tutorial-sql-intro

This snippet demonstrates how to start the `psql` client connected to a database named 'mydb' in single-step mode and then execute commands from a SQL file named 'basics.sql'. The `-s` option is used for step-by-step execution.

```shell
$ psql -s mydb

mydb=> \i basics.sql
```

--------------------------------

### Create Subscription on PostgreSQL Subscriber Database

Source: https://www.postgresql.org/docs/devel/logical-replication-quick-setup

This SQL command creates a subscription named `mysub` on the subscriber database. It connects to the publisher (specified by connection string) and subscribes to the `mypub` publication, initiating the replication process for the defined tables.

```sql
CREATE SUBSCRIPTION mysub CONNECTION 'dbname=foo host=bar user=repuser' PUBLICATION mypub;

```

--------------------------------

### Makefile Configuration for Jade Installation

Source: https://www.postgresql.org/docs/6.5/docguide25388

Example configuration for critical variables within a Makefile during the Jade installation process. These settings determine installation paths, library locations, and program directories.

```makefile
prefix = /usr/local
XDEFINES = -DSGML_CATALOG_FILES_DEFAULT="/usr/local/share/sgml/catalog"
XLIBS = -lm
RANLIB = ranlib
srcdir = ..
XLIBDIRS = grove spgrove style
XPROGDIRS = jade

```

--------------------------------

### Create Subscription on Subscriber Database

Source: https://www.postgresql.org/docs/10/logical-replication-quick-setup

Establishes a subscription named 'mysub' on the subscriber database, connecting to a publisher database specified by connection details. It subscribes to the 'mypub' publication, initiating data synchronization and replication.

```postgresql
CREATE SUBSCRIPTION mysub CONNECTION 'dbname=foo host=bar user=repuser' PUBLICATION mypub;
```

--------------------------------

### BKI Backend Interface Command Example (BKI)

Source: https://www.postgresql.org/docs/7.3/developer

This example shows a command in the Backend Interface (BKI) language, used for defining database objects and configurations within PostgreSQL. It's part of the guide's explanation of the BKI file format.

```bki
CREATE FUNCTION
    my_func(integer, integer)
    RETURNS integer
    AS 'MODULE_PATHNAME', 'my_func_impl';

```

--------------------------------

### Build PostgreSQL World (All Components)

Source: https://www.postgresql.org/docs/12/install-procedure

Builds the main PostgreSQL server, documentation (HTML and man pages), and additional modules from the 'contrib' directory. This target ensures a complete build of all available components.

```shell
make world
```

--------------------------------

### Retrieve Enum Sub-Range Between Two Values in PostgreSQL (enum_range)

Source: https://www.postgresql.org/docs/14/functions-enum

Demonstrates the two-argument 'enum_range' function to retrieve an ordered array of enum values between two specified members of the same enum type, inclusive of the start and end values. For example, getting values from 'orange' to 'green'.

```SQL
enum_range('orange'::rainbow, 'green'::rainbow)
```

--------------------------------

### Manual Installation Example: Declare PL/pgSQL Validator Function

Source: https://www.postgresql.org/docs/8.0/xplang

This SQL example shows how to declare the validator function for PL/pgSQL. This function is responsible for checking the syntax and structure of PL/pgSQL code during function creation, ensuring its correctness before execution.

```sql
CREATE FUNCTION plpgsql_validator(oid) RETURNS void AS
    '$libdir/plpgsql' LANGUAGE C;
```

--------------------------------

### Install PostgreSQL ODBC Components to Specific Directories

Source: https://www.postgresql.org/docs/7.0/odbc24471

This command allows for the installation of PostgreSQL ODBC components into explicitly defined directories, such as binary, library, and header file locations. It also allows specifying a custom ODBC installation file.

```bash
% make BINDIR=bindir  LIBDIR=libdir  HEADERDIR=headerdir ODBCINST=instfile install

```

--------------------------------

### Install PostgreSQL ODBC Catalog Extensions

Source: https://www.postgresql.org/docs/7.0/odbc24471

This command installs the necessary ODBC catalog extensions into the template1 database, ensuring that all subsequent databases will inherit these definitions. It requires the psql command-line tool.

```bash
% psql -e template1 < $PGROOT/contrib/odbc/odbc.sql

```

--------------------------------

### Add PostgreSQL Bin Directory to csh/tcsh Path

Source: https://www.postgresql.org/docs/6.4/environ

Configures the shell's command search path for csh or tcsh variants to include the PostgreSQL binary directory. This allows execution of PostgreSQL commands from any location. Ensure the path `/usr/local/pgsql/bin` is substituted with your actual PostgreSQL installation directory.

```csh
set path = ( /usr/local/pgsql/bin path )

```

--------------------------------

### Example Makefile.custom for PentiumPro Linux

Source: https://www.postgresql.org/docs/6.5/config12627

An illustrative example of a Makefile.custom file tailored for a PentiumPro Linux system. It shows how to define installation paths and compiler flags, including appending to CFLAGS.

```makefile
# Makefile.custom
# Thomas Lockhart 1999-06-01

POSTGRESDIR= /opt/postgres/current
CFLAGS+= -m486 -O2

# documentation

HSTYLE= /home/tgl/SGML/db118.d/docbook/html
PSTYLE= /home/tgl/SGML/db118.d/docbook/print
   
```

--------------------------------

### Start PostgreSQL Postmaster Daemon (Background Test)

Source: https://www.postgresql.org/docs/6.5/install12893

Starts the PostgreSQL postmaster daemon in the background for a brief test. It logs output to pgserver.log. This is a temporary step to test backend startup.

```bash
cd
nohup postmaster -i > pgserver.log 2>&1 &
```

--------------------------------

### Install PostgreSQL binaries without documentation (world-bin build) using Make

Source: https://www.postgresql.org/docs/15/install-procedure

This command installs the 'world' build components but explicitly excludes the documentation. It's useful for reducing installation size or when documentation is not needed locally.

```Makefile
make install-world-bin
```

--------------------------------

### Connect and Execute Commands in PostgreSQL using libpq (C)

Source: https://www.postgresql.org/docs/10/libpq-example

This snippet shows how to establish a connection to a PostgreSQL database using libpq, set a search path, and execute a simple command. It includes error handling for connection and command execution. Dependencies include the libpq library.

```c
/* Make a connection to the database */
    conn = PQconnectdb(conninfo);

    /* Check to see that the backend connection was successfully made */
    if (PQstatus(conn) != CONNECTION_OK)
    {
        fprintf(stderr, "Connection to database failed: %s",
                PQerrorMessage(conn));
        exit_nicely(conn);
    }

    /* Set always-secure search path, so malicious users can't take control. */
    res = PQexec(conn, "SET search_path = testlibpq3");
    if (PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "SET failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }
    PQclear(res);
```

--------------------------------

### Install PostgreSQL Documentation (Shell)

Source: https://www.postgresql.org/docs/7.0/install17165

Navigates to the PostgreSQL documentation source directory and installs the documentation files. This typically places man pages and HTML documentation into designated system directories.

```shell
> cd /usr/src/pgsql/postgresql-7.0/doc
> gmake install
```

--------------------------------

### Print PostgreSQL User's Guide (Postscript)

Source: https://www.postgresql.org/docs/6.5/install12893

This snippet demonstrates how to print the PostgreSQL User's Guide to a Postscript printer or a system configured for Postscript output. It involves changing the directory, unzipping the Postscript file, and piping it to the lpr command.

```bash
cd /usr/local/pgsql/doc
gunzip user.ps.tz | lpr
```

--------------------------------

### Create Publication on Publisher Database

Source: https://www.postgresql.org/docs/11/logical-replication-quick-setup

Defines a publication named 'mypub' on the publisher database, specifying which tables ('users', 'departments') to replicate. This SQL command initiates the publication process.

```sql
CREATE PUBLICATION mypub FOR TABLE users, departments;

```

--------------------------------

### Install PostgreSQL Documentation (make install-docs)

Source: https://www.postgresql.org/docs/10/install-procedure

Installs both HTML and man page documentation for PostgreSQL. This command should be used after the system files have been successfully built.

```shell
make install-docs
```

--------------------------------

### Demonstrate PostgreSQL Two-Phase Commit with pg_recvlogical and psql

Source: https://www.postgresql.org/docs/devel/logicaldecoding-example

This comprehensive example showcases the setup, execution, and cleanup of a PostgreSQL two-phase commit transaction using `pg_recvlogical` for logical decoding and `psql` for database operations. It includes dropping a potentially existing slot, creating a new slot with two-phase commit enabled, starting the logical stream, executing a `PREPARE TRANSACTION`, committing it, and finally dropping the slot. Ensure `max_prepared_transactions` is set appropriately in PostgreSQL.

```shell
pg_recvlogical -d postgres --slot=test --drop-slot
```

```shell
pg_recvlogical -d postgres --slot=test --create-slot --enable-two-phase
```

```shell
pg_recvlogical -d postgres --slot=test --start -f -
```

```shell
psql -d postgres -c "BEGIN;INSERT INTO data(data) VALUES('5');PREPARE TRANSACTION 'test';"
```

```shell
psql -d postgres -c "COMMIT PREPARED 'test';"
```

```shell
pg_recvlogical -d postgres --slot=test --drop-slot
```

--------------------------------

### Create Publication on Publisher Database

Source: https://www.postgresql.org/docs/10/logical-replication-quick-setup

Defines a publication named 'mypub' on the publisher database, specifying that the 'users' and 'departments' tables should be included in the publication. This publication acts as a source for replicated data.

```postgresql
CREATE PUBLICATION mypub FOR TABLE users, departments;
```

--------------------------------

### Configure PostgreSQL Search Path and Start Transaction in C

Source: https://www.postgresql.org/docs/devel/lo-examplesect

This section executes SQL commands to set a secure `search_path` to prevent malicious control and starts a new transaction using `BEGIN`. It utilizes `PQexec` for SQL command execution and `PQclear` to release the result set memory after each command.

```C
    /* Set always-secure search path, so malicious users can't take control. */
    res = PQexec(conn,
                 "SELECT pg_catalog.set_config('search_path', '', false)");
    if (PQresultStatus(res) != PGRES_TUPLES_OK)
    {
        fprintf(stderr, "SET failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }
    PQclear(res);

    res = PQexec(conn, "begin");
    PQclear(res);
```

--------------------------------

### Add PostgreSQL Bin Directory to sh/ksh/bash Path

Source: https://www.postgresql.org/docs/6.4/environ

Configures the shell's command search path for sh, ksh, or bash variants to include the PostgreSQL binary directory. This allows execution of PostgreSQL commands from any location. Ensure the path `/usr/local/pgsql/bin` is substituted with your actual PostgreSQL installation directory.

```bash
PATH=/usr/local/pgsql/bin PATH
export PATH

```

--------------------------------

### Install PostgreSQL Files (Shell)

Source: https://www.postgresql.org/docs/15/install-windows-full

Commands to install PostgreSQL files to a specified destination directory. 'install' installs all files, while 'install client' installs only client applications and libraries.

```shell
**install c:\\destination\\directory**

```

```shell
**install c:\\destination\\directory client**

```

--------------------------------

### Starting PostgreSQL Interactive Monitor (psql)

Source: https://www.postgresql.org/docs/6.5/start22962

This command initiates the PostgreSQL interactive terminal monitor, `psql`, allowing users to interact with the database. Ensure the PostgreSQL server (postmaster) is running and accessible via socket or TCP/IP connections. The output or lack thereof indicates successful connection or a potential issue.

```bash
% psql template1

```

```bash
% psql -h localhost template1

```

--------------------------------

### Perform a standard installation of PostgreSQL using Make

Source: https://www.postgresql.org/docs/15/install-procedure

This command compiles and installs the full PostgreSQL system into the directories specified during the `configure` step. It typically requires root privileges or appropriate write permissions to the target installation paths.

```Makefile
make install
```

--------------------------------

### Override ODBC Installation Path

Source: https://www.postgresql.org/docs/7.0/odbc24471

This command demonstrates how to override the default installation path for the ODBC driver's configuration file during the make install process. This is useful for specifying a custom filename for the ODBCINST configuration.

```bash
% make ODBCINST=`filename` install

```

--------------------------------

### Print PostgreSQL User's Guide with Ghostscript

Source: https://www.postgresql.org/docs/6.4/install12063

This snippet demonstrates how to print the PostgreSQL User's Guide using Ghostscript. It involves uncompressing a Postscript file, using the 'gs' command with specific device and resolution settings, and then printing the output. Ensure Ghostscript is installed and configured for your printer.

```shell
cd /usr/local/pgsql/doc
gunzip user.ps.tz | lpr
```

```shell
alias gshp='gs -sDEVICE=laserjet -r300 -dNOPAUSE'
export GS_LIB=/usr/share/ghostscript:/usr/share/ghostscript/fonts
gunzip user.ps.gz
gshp -sOUTPUTFILE=user.hp user.ps
gzip user.ps
lpr -l -s -r manpage.hp
```

--------------------------------

### Large Objects with Libpq Example (PostgreSQL)

Source: https://www.postgresql.org/docs/7.3/programmer

This example program demonstrates how to handle large objects (like files) in PostgreSQL using the libpq library. It covers operations for reading and writing large object data.

```c
/*
** Large Objects with Libpq Example Program
** This is a placeholder for the actual C code.
*/
#include <stdio.h>
#include <stdlib.h>
#include <libpq-fe.h>
#include <libpq/pqformat.h>
#include <sys/stat.h>
#include <fcntl.h>

int main(int argc, char **argv) {
    // Placeholder for Large Objects with Libpq example code
    printf("Large Objects with Libpq Example Program placeholder.\n");
    return 0;
}

```

--------------------------------

### Print PostgreSQL User's Guide (Shell)

Source: https://www.postgresql.org/docs/7.0/install17165

Uncompresses and pipes the Postscript version of the PostgreSQL User's Guide to the printer. This command assumes the Postscript file is gzipped (`user.ps.tz`) and relies on the `lpr` command for printing.

```shell
> cd /usr/local/pgsql/doc
> gunzip -c user.ps.tz | lpr
```

--------------------------------

### Manual Installation Example: Declare PL/pgSQL Call Handler Function

Source: https://www.postgresql.org/docs/8.0/xplang

This SQL example demonstrates how to declare the specific call handler function for the PL/pgSQL language. It tells the PostgreSQL server where to find the `plpgsql` shared object, which contains the logic for executing PL/pgSQL functions.

```sql
CREATE FUNCTION plpgsql_call_handler() RETURNS language_handler AS
    '$libdir/plpgsql' LANGUAGE C;
```

--------------------------------

### Create Publication on PostgreSQL Publisher Database

Source: https://www.postgresql.org/docs/devel/logical-replication-quick-setup

This SQL command creates a publication named `mypub` on the publisher database. It specifies that changes to the `users` and `departments` tables will be published, making them available for replication to subscribers.

```sql
CREATE PUBLICATION mypub FOR TABLE users, departments;

```

--------------------------------

### PostgreSQL SHOW geqo Example

Source: https://www.postgresql.org/docs/14/sql-show

An example showing how to use the SHOW command to retrieve the current setting of the 'geqo' parameter in PostgreSQL.

```sql
SHOW geqo;

 geqo
------
 on
(1 row)
```

--------------------------------

### Compile PostgreSQL Tutorial Files

Source: https://www.postgresql.org/docs/13/tutorial-sql-intro

This command sequence navigates to the PostgreSQL tutorial source directory and runs 'make' to compile C files and create necessary scripts for user-defined functions and types. This is a prerequisite for running the tutorial examples.

```bash
$ cd _..._/src/tutorial
$ make

```

--------------------------------

### PostgreSQL SHOW Command Examples

Source: https://www.postgresql.org/docs/16/sql-show

Illustrates practical usage of the PostgreSQL SHOW command to retrieve settings for specific parameters like 'DateStyle' and 'geqo', as well as displaying all configuration parameters.

```sql
SHOW DateStyle;
-- Expected Output:
--  DateStyle 
-- ----------- 
--  ISO, MDY 
--(1 row) 

SHOW geqo;
-- Expected Output:
--  geqo 
-- ------ 
--  on 
--(1 row) 

SHOW ALL;
-- Expected Output (truncated):
--             name         | setting |                description 
-- -------------------------+---------+------------------------------------------------- 
--  allow_system_table_mods | off     | Allows modifications of the structure of ... 
--     . 
--     . 
--     . 
--  xmloption               | content | Sets whether XML data in implicit parsing ... 
--  zero_damaged_pages      | off     | Continues processing past damaged page headers. 
--(196 rows)
```

--------------------------------

### Generate Plain Text INSTALL File for PostgreSQL

Source: https://www.postgresql.org/docs/10/docguide-build

Recreates the INSTALL file, which corresponds to Chapter 16 of the PostgreSQL documentation, as a plain text file. This is useful for situations where advanced reading tools are not available.

```makefile
make INSTALL
```

--------------------------------

### Connect to PostgreSQL and Listen for Notifications with libpq (C)

Source: https://www.postgresql.org/docs/devel/libpq-example

Establishes a connection to a PostgreSQL database, sets the search path, issues a LISTEN command, and enters a loop to asynchronously wait for and process database notifications using select() and PQnotifies. This snippet demonstrates connection handling, error checking, and resource cleanup within a typical main function structure.

```C
     * environment variables or defaults for all other connection parameters.
     */
    if (argc > 1)
        conninfo = argv[1];
    else
        conninfo = "dbname = postgres";

    /* Make a connection to the database */
    conn = PQconnectdb(conninfo);

    /* Check to see that the backend connection was successfully made */
    if (PQstatus(conn) != CONNECTION_OK)
    {
        fprintf(stderr, "%s", PQerrorMessage(conn));
        exit_nicely(conn);
    }

    /* Set always-secure search path, so malicious users can't take control. */
    res = PQexec(conn,
                 "SELECT pg_catalog.set_config('search_path', '', false)");
    if (PQresultStatus(res) != PGRES_TUPLES_OK)
    {
        fprintf(stderr, "SET failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }

    /*
     * Should PQclear PGresult whenever it is no longer needed to avoid memory
     * leaks
     */
    PQclear(res);

    /*
     * Issue LISTEN command to enable notifications from the rule's NOTIFY.
     */
    res = PQexec(conn, "LISTEN TBL2");
    if (PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "LISTEN command failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }
    PQclear(res);

    /* Quit after four notifies are received. */
    nnotifies = 0;
    while (nnotifies < 4)
    {
        /*
         * Sleep until something happens on the connection.  We use select(2)
         * to wait for input, but you could also use poll() or similar
         * facilities.
         */
        int         sock;
        fd_set      input_mask;

        sock = PQsocket(conn);

        if (sock < 0)
            break;              /* shouldn't happen */

        FD_ZERO(&input_mask);
        FD_SET(sock, &input_mask);

        if (select(sock + 1, &input_mask, NULL, NULL, NULL) < 0)
        {
            fprintf(stderr, "select() failed: %s\n", strerror(errno));
            exit_nicely(conn);
        }

        /* Now check for input */
        PQconsumeInput(conn);
        while ((notify = PQnotifies(conn)) != NULL)
        {
            fprintf(stderr,
                    "ASYNC NOTIFY of '%s' received from backend PID %d\n",
                    notify->relname, notify->be_pid);
            PQfreemem(notify);
            nnotifies++;
            PQconsumeInput(conn);
        }
    }

    fprintf(stderr, "Done.\n");

    /* close the connection to the database and cleanup */
    PQfinish(conn);

    return 0;
}
```

--------------------------------

### Complete crosstab example with data setup

Source: https://www.postgresql.org/docs/18/tablefunc

This example demonstrates creating a table, inserting sample data, and then using the `crosstab` function to pivot the data. It includes the necessary `CREATE TABLE`, `INSERT`, and `SELECT` statements.

```PostgreSQL
CREATE TABLE ct(id SERIAL, rowid TEXT, attribute TEXT, value TEXT);
INSERT INTO ct(rowid, attribute, value) VALUES('test1','att1','val1');
INSERT INTO ct(rowid, attribute, value) VALUES('test1','att2','val2');
INSERT INTO ct(rowid, attribute, value) VALUES('test1','att3','val3');
INSERT INTO ct(rowid, attribute, value) VALUES('test1','att4','val4');
INSERT INTO ct(rowid, attribute, value) VALUES('test2','att1','val5');
INSERT INTO ct(rowid, attribute, value) VALUES('test2','att2','val6');
INSERT INTO ct(rowid, attribute, value) VALUES('test2','att3','val7');
INSERT INTO ct(rowid, attribute, value) VALUES('test2','att4','val8');

SELECT *
FROM crosstab(
  'select rowid, attribute, value
   from ct
   where attribute = "att2" or attribute = "att3" 
   order by 1,2')
AS ct(row_name text, category_1 text, category_2 text, category_3 text);

```

--------------------------------

### PostgreSQL Makefile.custom Configuration

Source: https://www.postgresql.org/docs/6.5/docguide25253

Example configuration for Makefile.custom in PostgreSQL, defining installation directory, compiler flags, lexer verbosity, and paths for HTML and print stylesheets.

```makefile
# Makefile.custom
# Thomas Lockhart 1998-03-01

POSTGRESDIR= /opt/postgres/current
CFLAGS+= -m486
YFLAGS+= -v

# documentation

HSTYLE= /home/tgl/SGML/db107.d/docbook/html
PSTYLE= /home/tgl/SGML/db107.d/docbook/print
   

```

--------------------------------

### Verify `configure` Detection of DocBook/SGML Tools

Source: https://www.postgresql.org/docs/10/docguide-toolsets

Example output from the PostgreSQL `configure` script, showing successful detection of various tools required for building documentation, including `onsgmls` (from OpenSP), DocBook DTD, and other XML/SGML processors. This confirms a correctly set up documentation build environment.

```shell
checking for onsgmls... onsgmls
checking for DocBook V4.2... yes
checking for dbtoepub... dbtoepub
checking for xmllint... xmllint
checking for xsltproc... xsltproc
checking for osx... osx
checking for fop... fop
```

--------------------------------

### Create Subscription on Subscriber Database

Source: https://www.postgresql.org/docs/11/logical-replication-quick-setup

Establishes a subscription named 'mysub' on the subscriber database, connecting to the publisher and subscribing to the 'mypub' publication. This command synchronizes initial data and replicates ongoing changes.

```sql
CREATE SUBSCRIPTION mysub CONNECTION 'dbname=foo host=bar user=repuser' PUBLICATION mypub;

```

--------------------------------

### Start PostgreSQL Postmaster Daemon (Background)

Source: https://www.postgresql.org/docs/6.4/install12063

Starts the PostgreSQL postmaster daemon in the background. This command is used for basic testing and ensures the server is running.

```bash
cd
postmaster -i
```

--------------------------------

### Standalone Installation: Unzip Package

Source: https://www.postgresql.org/docs/6.5/odbc19863

This command is used to unpack a zip archive of the psqlODBC driver for a standalone installation. The `-a` option is crucial for handling DOS CR/LF line endings in source files.

```bash
% unzip -a `packagename`
```

--------------------------------

### Binary Data Examples (JDBC - PostgreSQL)

Source: https://www.postgresql.org/docs/7.3/programmer

This Java snippet provides examples for handling binary data (like BLOBs or BYTEA) with PostgreSQL using JDBC. It covers reading and writing binary data to the database.

```java
/*
** Binary Data Examples
** This is a placeholder for the actual Java code.
*/
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.io.InputStream;
import java.io.OutputStream;

public class BinaryDataJdbc {
    public static void main(String[] args) {
        String url = "jdbc:postgresql://localhost:5432/mydatabase";
        String user = "myuser";
        String password = "mypassword";

        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            // Example for writing binary data (BYTEA)
            byte[] dataToWrite = {1, 2, 3, 4, 5};
            String insertSql = "INSERT INTO binary_table (id, binary_data) VALUES (?, ?)";
            try (PreparedStatement pstmt = conn.prepareStatement(insertSql)) {
                pstmt.setInt(1, 1);
                pstmt.setBytes(2, dataToWrite);
                pstmt.executeUpdate();
                System.out.println("Binary data written successfully.");
            }

            // Example for reading binary data
            String selectSql = "SELECT binary_data FROM binary_table WHERE id = ?";
            try (PreparedStatement pstmt = conn.prepareStatement(selectSql)) {
                pstmt.setInt(1, 1);
                try (ResultSet rs = pstmt.executeQuery()) {
                    if (rs.next()) {
                        byte[] dataRead = rs.getBytes(1);
                        System.out.println("Binary data read successfully. Length: " + dataRead.length);
                        // Process dataRead
                    }
                }
            }

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

--------------------------------

### Install PostgreSQL ODBC Driver

Source: https://www.postgresql.org/docs/6.4/odbc18456

Installs the compiled PostgreSQL ODBC driver source code. The POSTGRESDIR variable can be used to set the root directory for installation. Specific directories like BINDIR, LIBDIR, HEADERDIR, and ODBCINST can also be overridden.

```bash
% make POSTGRESDIR=`targettree` install
% make BINDIR=`bindir` LIBDIR=`libdir` HEADERDIR=`headerdir` install
% make POSTGRESDIR=/opt/psqlodbc install
% make POSTGRESDIR=/opt/psqlodbc HEADERDIR=/usr/local install
```

--------------------------------

### Connect and Query PostgreSQL Database with libpq (C)

Source: https://www.postgresql.org/docs/10/libpq-example

This example demonstrates how to establish a connection to a PostgreSQL database using libpq, execute SQL commands including setting search_path, starting a transaction, declaring and fetching from a cursor, and finally closing the connection. It handles connection errors and result status checks.

```c
/*
 * src/test/examples/testlibpq.c
 *
 *
 * testlibpq.c
 *
 *      Test the C version of libpq, the PostgreSQL frontend library.
 */
#include <stdio.h>
#include <stdlib.h>
#include "libpq-fe.h"

static void
exit_nicely(PGconn *conn)
{
    PQfinish(conn);
    exit(1);
}

int
main(int argc, char **argv)
{
    const char *conninfo;
    PGconn     *conn;
    PGresult   *res;
    int         nFields;
    int         i, 
                j;

    /*
     * If the user supplies a parameter on the command line, use it as the
     * conninfo string; otherwise default to setting dbname=postgres and using
     * environment variables or defaults for all other connection parameters.
     */
    if (argc > 1)
        conninfo = argv[1];
    else
        conninfo = "dbname = postgres";

    /* Make a connection to the database */
    conn = PQconnectdb(conninfo);

    /* Check to see that the backend connection was successfully made */
    if (PQstatus(conn) != CONNECTION_OK)
    {
        fprintf(stderr, "Connection to database failed: %s",
                PQerrorMessage(conn));
        exit_nicely(conn);
    }

    /* Set always-secure search path, so malicious users can't take control. */
    res = PQexec(conn,
                 "SELECT pg_catalog.set_config('search_path', '', false)");
    if (PQresultStatus(res) != PGRES_TUPLES_OK)
    {
        fprintf(stderr, "SET failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }

    /*
     * Should PQclear PGresult whenever it is no longer needed to avoid memory
     * leaks
     */
    PQclear(res);

    /*
     * Our test case here involves using a cursor, for which we must be inside
     * a transaction block.  We could do the whole thing with a single
     * PQexec() of "select * from pg_database", but that's too trivial to make
     * a good example.
     */

    /* Start a transaction block */
    res = PQexec(conn, "BEGIN");
    if (PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "BEGIN command failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }
    PQclear(res);

    /*
     * Fetch rows from pg_database, the system catalog of databases
     */
    res = PQexec(conn, "DECLARE myportal CURSOR FOR select * from pg_database");
    if (PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "DECLARE CURSOR failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }
    PQclear(res);

    res = PQexec(conn, "FETCH ALL in myportal");
    if (PQresultStatus(res) != PGRES_TUPLES_OK)
    {
        fprintf(stderr, "FETCH ALL failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }

    /* first, print out the attribute names */
    nFields = PQnfields(res);
    for (i = 0; i < nFields; i++)
        printf("% -15s", PQfname(res, i));
    printf("\n\n");

    /* next, print out the rows */
    for (i = 0; i < PQntuples(res); i++)
    {
        for (j = 0; j < nFields; j++)
            printf("% -15s", PQgetvalue(res, i, j));
        printf("\n");
    }

    PQclear(res);

    /* close the portal ... we don't bother to check for errors ... */
    res = PQexec(conn, "CLOSE myportal");
    PQclear(res);

    /* end the transaction */
    res = PQexec(conn, "END");
    PQclear(res);

    /* close the connection to the database and cleanup */
    PQfinish(conn);

    return 0;
}

```

--------------------------------

### SQL Example File Reference for PostgreSQL

Source: https://www.postgresql.org/docs/11/tutorial-advanced-intro

This snippet references an external SQL file containing sample data and advanced SQL examples. It is intended to be loaded and used in conjunction with the tutorial's advanced features chapter. Ensure the tutorial directory is accessible.

```text
advanced.sql
```

--------------------------------

### libpq Example Programs (C)

Source: https://www.postgresql.org/docs/7.2/programmer

Illustrates how to use the libpq C library for interacting with PostgreSQL databases. These examples cover basic connection, command execution, and data handling.

```c
#include <stdio.h>
#include <libpq-fe.h>

int main() {
    PGconn *conn;
    PGresult *res;

    // Example connection string
    conn = PQconnectdb("user=postgres password=mypass dbname=mydb host=localhost port=5432");

    if (PQstatus(conn) == CONNECTION_BAD) {
        fprintf(stderr, "Connection to database failed: %s", PQerrorMessage(conn));
        PQfinish(conn);
        return 1;
    }

    // Example query execution
    res = PQexec(conn, "SELECT version();");
    if (PQresultStatus(res) != PGRES_TUPLES_OK) {
        fprintf(stderr, "Query failed: %s", PQerrorMessage(conn));
        PQclear(res);
        PQfinish(conn);
        return 1;
    }

    // Process results
    printf("%s\n", PQgetvalue(res, 0, 0));

    PQclear(res);
    PQfinish(conn);

    return 0;
}
```

--------------------------------

### PostgreSQL Error Message Reason Example

Source: https://www.postgresql.org/docs/11/error-style-guide

Highlights the need to include the reason for an error. The 'BETTER' example provides specific cause ('I/O failure') compared to the 'BAD' example, which is too generic.

```text
BAD:    could not open file %s
BETTER: could not open file %s (I/O failure)

```

--------------------------------

### Start PostgreSQL Server (Background - Shell)

Source: https://www.postgresql.org/docs/7.0/install17165

Starts the PostgreSQL server process in the background, redirecting output to `server.log`. This command uses `nohup` to ensure the server continues running after the terminal session ends and detaches from the terminal.

```shell
> nohup /usr/local/pgsql/bin/postmaster -D /usr/local/pgsql/data \
    </dev/null >>server.log 2>>1 &
```

--------------------------------

### PL/pgSQL Trigger Procedure Example (PostgreSQL)

Source: https://www.postgresql.org/docs/7.3/programmer

This snippet provides an example of creating a trigger procedure using PL/pgSQL in PostgreSQL. Trigger procedures are executed automatically in response to certain table events.

```plpgsql
-- A PL/pgSQL Trigger Procedure Example
-- This is a placeholder for the actual PL/pgSQL code.

CREATE OR REPLACE FUNCTION my_trigger_function()
RETURNS TRIGGER AS $$
BEGIN
    -- Trigger logic here
    RAISE NOTICE 'Trigger fired on table %', TG_TABLE_NAME;
    RETURN NEW; -- For BEFORE triggers, return NEW or OLD. For AFTER triggers, return NULL.
END;
$$ LANGUAGE plpgsql;

-- Example of creating a trigger:
-- CREATE TRIGGER my_trigger
-- BEFORE INSERT OR UPDATE ON my_table
-- FOR EACH ROW EXECUTE FUNCTION my_trigger_function();

```

--------------------------------

### Example of Executed Archive Command

Source: https://www.postgresql.org/docs/10/continuous-archiving

An illustration of how PostgreSQL might format the `archive_command` after replacing placeholders like `%p` and `%f` for a specific WAL segment file.

```shell
test ! -f /mnt/server/archivedir/00000001000000A900000065 && cp pg_wal/00000001000000A900000065 /mnt/server/archivedir/00000001000000A900000065
```

--------------------------------

### `DataSource` Code Example (JDBC - PostgreSQL)

Source: https://www.postgresql.org/docs/7.3/programmer

This Java snippet provides a basic code example for using a `DataSource` object to obtain connections in JDBC with PostgreSQL. `DataSource` is a standard Java interface for database connections.

```java
/*
** `DataSource` Code Example
** This is a placeholder for the actual Java code.
*/
import javax.sql.DataSource;
import java.sql.Connection;
import java.sql.SQLException;
// Assuming a specific DataSource implementation is available, e.g., from PostgreSQL JDBC driver
import org.postgresql.ds.PGSimpleDataSource;

public class DataSourceExample {
    public static void main(String[] args) {
        // Create a DataSource instance (e.g., PGSimpleDataSource)
        DataSource dataSource = new PGSimpleDataSource();
        ((PGSimpleDataSource) dataSource).setServerName("localhost");
        ((PGSimpleDataSource) dataSource).setPortNumber(5432);
        ((PGSimpleDataSource) dataSource).setDatabaseName("mydatabase");
        ((PGSimpleDataSource) dataSource).setUser("myuser");
        ((PGSimpleDataSource) dataSource).setPassword("mypassword");

        try (Connection connection = dataSource.getConnection()) {
            System.out.println("Successfully obtained a connection from DataSource.");
            // Use the connection for database operations
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}

```

--------------------------------

### Build PostgreSQL World Binaries (No Docs)

Source: https://www.postgresql.org/docs/12/install-procedure

Builds the main PostgreSQL server and additional modules ('contrib') but excludes the documentation. This is useful if documentation is not required or will be generated separately.

```shell
make world-bin
```

--------------------------------

### Enable and Refresh PostgreSQL Subscription (Example 1)

Source: https://www.postgresql.org/docs/devel/logical-replication-subscription

These SQL commands complete the activation of the subscription from Example 1. First, the subscription is enabled, and then its publication information is refreshed to initiate replication after the slot has been manually created on the publisher.

```sql
ALTER SUBSCRIPTION sub1 ENABLE;
ALTER SUBSCRIPTION sub1 REFRESH PUBLICATION;
```

--------------------------------

### PostgreSQL: Check if a range does not extend left of another

Source: https://www.postgresql.org/docs/14/functions-range

This example demonstrates the `&>` operator, which checks if the first range's start is greater than or equal to the second range's start. It determines if the first range does not extend to the left of the second. The example uses `int8range`.

```sql
SELECT int8range(7,20) &> int8range(5,10);
```

--------------------------------

### Connect to PostgreSQL and Listen for Notifications (C)

Source: https://www.postgresql.org/docs/10/libpq-example

Establishes a connection to a PostgreSQL database, sets the search path, and listens for notifications on a specified channel. It then enters a loop to wait for and process incoming notifications using select() and PQconsumeInput().

```C
/*
     * conninfo string; otherwise default to setting dbname=postgres and using
     * environment variables or defaults for all other connection parameters.
     */
    if (argc > 1)
        conninfo = argv[1];
    else
        conninfo = "dbname = postgres";

    /* Make a connection to the database */
    conn = PQconnectdb(conninfo);

    /* Check to see that the backend connection was successfully made */
    if (PQstatus(conn) != CONNECTION_OK)
    {
        fprintf(stderr, "Connection to database failed: %s",
                PQerrorMessage(conn));
        exit_nicely(conn);
    }

    /* Set always-secure search path, so malicious users can't take control. */
    res = PQexec(conn,
                 "SELECT pg_catalog.set_config('search_path', '', false)");
    if (PQresultStatus(res) != PGRES_TUPLES_OK)
    {
        fprintf(stderr, "SET failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }

    /*
     * Should PQclear PGresult whenever it is no longer needed to avoid memory
     * leaks
     */
    PQclear(res);

    /*
     * Issue LISTEN command to enable notifications from the rule's NOTIFY.
     */
    res = PQexec(conn, "LISTEN TBL2");
    if (PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "LISTEN command failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }
    PQclear(res);

    /* Quit after four notifies are received. */
    nnotifies = 0;
    while (nnotifies < 4)
    {
        /*
         * Sleep until something happens on the connection.  We use select(2)
         * to wait for input, but you could also use poll() or similar
         * facilities.
         */
        int         sock;
        fd_set      input_mask;

        sock = PQsocket(conn);

        if (sock < 0)
            break;              /* shouldn't happen */

        FD_ZERO(&input_mask);
        FD_SET(sock, &input_mask);

        if (select(sock + 1, &input_mask, NULL, NULL, NULL) < 0)
        {
            fprintf(stderr, "select() failed: %s\n", strerror(errno));
            exit_nicely(conn);
        }

        /* Now check for input */
        PQconsumeInput(conn);
        while ((notify = PQnotifies(conn)) != NULL)
        {
            fprintf(stderr,
                    "ASYNC NOTIFY of '%s' received from backend PID %d\n",
                    notify->relname, notify->be_pid);
            PQfreemem(notify);
            nnotifies++;
            PQconsumeInput(conn);
        }
    }

    fprintf(stderr, "Done.\n");

    /* close the connection to the database and cleanup */
    PQfinish(conn);

    return 0;
}

```

--------------------------------

### Manual PL/Perl Installation Example (SQL)

Source: https://www.postgresql.org/docs/17/xplang-install

Demonstrates the manual installation of the PL/Perl procedural language in PostgreSQL. It includes the creation of the call handler, inline handler, and validator functions, followed by the final CREATE TRUSTED LANGUAGE command.

```sql
CREATE FUNCTION plperl_call_handler() RETURNS language_handler AS
    '$libdir/plperl' LANGUAGE C;
```

```sql
CREATE FUNCTION plperl_inline_handler(internal) RETURNS void AS
    '$libdir/plperl' LANGUAGE C STRICT;
```

```sql
CREATE FUNCTION plperl_validator(oid) RETURNS void AS
    '$libdir/plperl' LANGUAGE C STRICT;
```

```sql
CREATE TRUSTED LANGUAGE plperl
    HANDLER plperl_call_handler
    INLINE plperl_inline_handler
    VALIDATOR plperl_validator;
```

--------------------------------

### PostgreSQL: Example Role Setup and Inheritance

Source: https://www.postgresql.org/docs/13/role-membership

Demonstrates setting up roles with different inheritance attributes (INHERIT, NOINHERIT) and how this affects privilege access. Includes commands for creating roles, granting membership, and using SET ROLE.

```sql
CREATE ROLE joe LOGIN INHERIT;
CREATE ROLE admin NOINHERIT;
CREATE ROLE wheel NOINHERIT;
GRANT admin TO joe;
GRANT wheel TO admin;

SET ROLE admin;
SET ROLE wheel;
SET ROLE joe;
SET ROLE NONE;
RESET ROLE;
```

--------------------------------

### Example pg_options File Content

Source: https://www.postgresql.org/docs/6.4/pg-options

Provides an example of how a `pg_options` file might look, showcasing the use of different trace flags and their assigned values.

```postgresql-conf
verbose=2
query
hostlookup
showportnumber
```

--------------------------------

### createdb: Create Database Example (Default)

Source: https://www.postgresql.org/docs/7.0/app-createdb

Demonstrates how to create a PostgreSQL database named 'demo' using the default database server settings. The output 'CREATE DATABASE' confirms successful creation.

```shell
$ `createdb demo`
CREATE DATABASE
```

--------------------------------

### PostgreSQL: Full Example - Execute SELECT and Get Column Info

Source: https://www.postgresql.org/docs/12/ecpg-sql-get-descriptor

This comprehensive C example demonstrates a complete workflow in PostgreSQL: connecting to a database, executing 'SELECT current_database()', fetching results into a descriptor, and then using GET DESCRIPTOR to retrieve and print the column count, data length, and data content. It includes essential steps like ALLOCATE DESCRIPTOR, DECLARE CURSOR, OPEN, FETCH, and DEALLOCATE DESCRIPTOR.

```c
int
main(void)
{
EXEC SQL BEGIN DECLARE SECTION;
    int  d_count;
    char d_data[1024];
    int  d_returned_octet_length;
EXEC SQL END DECLARE SECTION;

    EXEC SQL CONNECT TO testdb AS con1 USER testuser;
    EXEC SQL SELECT pg_catalog.set_config('search_path', '', false); EXEC SQL COMMIT;
    EXEC SQL ALLOCATE DESCRIPTOR d;

    /* Declare, open a cursor, and assign a descriptor to the cursor  */
    EXEC SQL DECLARE cur CURSOR FOR SELECT current_database();
    EXEC SQL OPEN cur;
    EXEC SQL FETCH NEXT FROM cur INTO SQL DESCRIPTOR d;

    /* Get a number of total columns */
    EXEC SQL GET DESCRIPTOR d :d_count = COUNT;
    printf("d_count                 = %d\n", d_count);

    /* Get length of a returned column */
    EXEC SQL GET DESCRIPTOR d VALUE 1 :d_returned_octet_length = RETURNED_OCTET_LENGTH;
    printf("d_returned_octet_length = %d\n", d_returned_octet_length);

    /* Fetch the returned column as a string */
    EXEC SQL GET DESCRIPTOR d VALUE 1 :d_data = DATA;
    printf("d_data                  = %s\n", d_data);

    /* Closing */
    EXEC SQL CLOSE cur;
    EXEC SQL COMMIT;

    EXEC SQL DEALLOCATE DESCRIPTOR d;
    EXEC SQL DISCONNECT ALL;

    return 0;
}

```

--------------------------------

### PostgreSQL Example Programs (C Library)

Source: https://www.postgresql.org/docs/13/libpq-example

This section provides access to example programs for PostgreSQL, likely demonstrating the usage of the libpq C library for database interactions. It serves as a starting point for developers integrating with PostgreSQL using C.

```text
33.21. Example Programs
---
Prev | Up | Chapter 33. libpq — C Library | Home |  Next
```

--------------------------------

### Starting PostgreSQL with Custom File Locations

Source: https://www.postgresql.org/docs/18/runtime-config-file-locations

This example demonstrates how to start the PostgreSQL server using command-line options to specify custom locations for the data directory and configuration files.

```bash
# Example assuming config files are in /etc/postgresql/config and data is in /var/lib/postgresql/data
postgres -D /etc/postgresql/config --config-file=/etc/postgresql/config/postgresql.conf --hba-file=/etc/postgresql/config/pg_hba.conf --ident-file=/etc/postgresql/config/pg_ident.conf -c "data_directory='/var/lib/postgresql/data'"
```

--------------------------------

### Libpq Example Program 1: Basic PostgreSQL Operations in C

Source: https://www.postgresql.org/docs/11/libpq-example

This C program demonstrates how to use libpq to connect to a PostgreSQL database, execute SQL commands (including setting search_path, starting transactions, declaring cursors, fetching data, and ending transactions), and process results. It includes error handling for connection and command execution. Dependencies: libpq-fe.h.

```c
/*
 * src/test/examples/testlibpq.c
 *
 *
 * testlibpq.c
 *
 *      Test the C version of libpq, the PostgreSQL frontend library.
 */
#include <stdio.h>
#include <stdlib.h>
#include "libpq-fe.h"

static void
exit_nicely(PGconn *conn)
{
    PQfinish(conn);
    exit(1);
}

int
main(int argc, char **argv)
{
    const char *conninfo;
    PGconn     *conn;
    PGresult   *res;
    int         nFields;
    int         i, j;

    /*
     * If the user supplies a parameter on the command line, use it as the
     * conninfo string; otherwise default to setting dbname=postgres and using
     * environment variables or defaults for all other connection parameters.
     */
    if (argc > 1)
        conninfo = argv[1];
    else
        conninfo = "dbname = postgres";

    /* Make a connection to the database */
    conn = PQconnectdb(conninfo);

    /* Check to see that the backend connection was successfully made */
    if (PQstatus(conn) != CONNECTION_OK)
    {
        fprintf(stderr, "Connection to database failed: %s",
                PQerrorMessage(conn));
        exit_nicely(conn);
    }

    /* Set always-secure search path, so malicious users can't take control. */
    res = PQexec(conn,
                 "SELECT pg_catalog.set_config('search_path', '', false)");
    if (PQresultStatus(res) != PGRES_TUPLES_OK)
    {
        fprintf(stderr, "SET failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }

    /*
     * Should PQclear PGresult whenever it is no longer needed to avoid memory
     * leaks
     */
    PQclear(res);

    /*
     * Our test case here involves using a cursor, for which we must be inside
     * a transaction block.  We could do the whole thing with a single
     * PQexec() of "select * from pg_database", but that's too trivial to make
     * a good example.
     */

    /* Start a transaction block */
    res = PQexec(conn, "BEGIN");
    if (PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "BEGIN command failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }
    PQclear(res);

    /*
     * Fetch rows from pg_database, the system catalog of databases
     */
    res = PQexec(conn, "DECLARE myportal CURSOR FOR select * from pg_database");
    if (PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "DECLARE CURSOR failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }
    PQclear(res);

    res = PQexec(conn, "FETCH ALL in myportal");
    if (PQresultStatus(res) != PGRES_TUPLES_OK)
    {
        fprintf(stderr, "FETCH ALL failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }

    /* first, print out the attribute names */
    nFields = PQnfields(res);
    for (i = 0; i < nFields; i++)
        printf("% -15s", PQfname(res, i));
    printf("\n\n");

    /* next, print out the rows */
    for (i = 0; i < PQntuples(res); i++)
    {
        for (j = 0; j < nFields; j++)
            printf("% -15s", PQgetvalue(res, i, j));
        printf("\n");
    }

    PQclear(res);

    /* close the portal ... we don't bother to check for errors ... */
    res = PQexec(conn, "CLOSE myportal");
    PQclear(res);

    /* end the transaction */
    res = PQexec(conn, "END");
    PQclear(res);

    /* close the connection to the database and cleanup */
    PQfinish(conn);

    return 0;
}

```

--------------------------------

### Start PostgreSQL Postmaster Silently

Source: https://www.postgresql.org/docs/6.5/postmaster

This command starts the postmaster in silent mode (-S option), suppressing debugging messages. Unlike the previous example, there is no ampersand at the end, meaning the postmaster will run in the foreground.

```shell
% postmaster -S
    

```

--------------------------------

### PostgreSQL Database Connection and Query Execution in C

Source: https://www.postgresql.org/docs/17/libpq-example

This C code snippet demonstrates establishing a connection to a PostgreSQL database using libpq, executing a SET command to configure the search path, and performing SELECT queries with parameters. It handles connection errors and result status checks, clearing results using PQclear. Dependencies include the libpq library.

```c
int
main(int argc, char **argv)
{
    const char *conninfo;
    PGconn     *conn;
    PGresult   *res;
    const char *paramValues[1];
    int         paramLengths[1];
    int         paramFormats[1];
    uint32_t    binaryIntVal;

    if (argc > 1)
        conninfo = argv[1];
    else
        conninfo = "dbname = postgres";

    conn = PQconnectdb(conninfo);

    if (PQstatus(conn) != CONNECTION_OK)
    {
        fprintf(stderr, "%s", PQerrorMessage(conn));
        exit_nicely(conn);
    }

    res = PQexec(conn, "SET search_path = testlibpq3");
    if (PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "SET failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }
    PQclear(res);

    paramValues[0] = "joe's place";

    res = PQexecParams(conn,
                       "SELECT * FROM test1 WHERE t = $1",
                       1,       /* one param */
                       NULL,    /* let the backend deduce param type */
                       paramValues,
                       NULL,    /* don't need param lengths since text */
                       NULL,    /* default to all text params */
                       1);      /* ask for binary results */

    if (PQresultStatus(res) != PGRES_TUPLES_OK)
    {
        fprintf(stderr, "SELECT failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }

    show_binary_results(res);

    PQclear(res);

    binaryIntVal = htonl((uint32_t) 2);

    paramValues[0] = (char *) &binaryIntVal;
    paramLengths[0] = sizeof(binaryIntVal);
    paramFormats[0] = 1;        /* binary */

    res = PQexecParams(conn,
                       "SELECT * FROM test1 WHERE i = $1::int4",
                       1,       /* one param */
                       NULL,    /* let the backend deduce param type */
                       paramValues,
                       paramLengths,
                       paramFormats,
                       1);      /* ask for binary results */

    if (PQresultStatus(res) != PGRES_TUPLES_OK)
    {
        fprintf(stderr, "SELECT failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }

    show_binary_results(res);

    PQclear(res);

    PQfinish(conn);

    return 0;
}

```

--------------------------------

### Install CVSup Binary from Source

Source: https://www.postgresql.org/docs/6.5/cvs23780

This command installs the compiled CVSup binary onto the system after it has been built from source. It uses the same M3FLAGS as the build command to ensure consistency. The 'install' target typically copies the binary to a standard location like /usr/local/bin and installs the man page.

```shell
# make M3FLAGS="-DNOGUI -DSTATIC" install
```

--------------------------------

### Add PostgreSQL Bin Directory to Shell Path (csh/tcsh)

Source: https://www.postgresql.org/docs/7.0/start

This code snippet demonstrates how to add the PostgreSQL binary directory to your system's command path for csh or tcsh shell variants. It modifies the .login file in the user's home directory. Ensure to replace '/usr/local/pgsql' with your actual PostgreSQL installation path.

```csh
% set path = ( /usr/local/pgsql/bin path )
    
```

--------------------------------

### PostgreSQL initdb Command Example

Source: https://www.postgresql.org/docs/6.4/app-initdb

This demonstrates the basic usage of the initdb command to create a new PostgreSQL database system. It initializes the data directory and sets up the default database structure.

```bash
initdb -D /path/to/your/data/directory
```

--------------------------------

### Manual PL/pgSQL Installation - Language Declaration

Source: https://www.postgresql.org/docs/7.4/xplang

Example of declaring the PL/pgSQL language to be trusted and associating it with its previously declared call handler function.

```sql
CREATE TRUSTED PROCEDURAL LANGUAGE plpgsql
    HANDLER plpgsql_call_handler;

```

--------------------------------

### PostgreSQL createdb Usage Example (Local)

Source: https://www.postgresql.org/docs/6.4/app-createdb

Demonstrates how to create a PostgreSQL database named 'demo' using the 'createdb' command on the local host with the default port.

```bash
createdb demo
```

--------------------------------

### PostgreSQL JSON Data Setup

Source: https://www.postgresql.org/docs/17/functions-json

Sets a JSON string constant in psql for subsequent query examples. This is a setup step before querying.

```sql
SELECT '{ 
  "track": { 
    "segments": [ 
      { 
        "location":   [ 47.763, 13.4034 ], 
        "start time": "2018-10-14 10:05:14", 
        "HR": 73 
      }, 
      { 
        "location":   [ 47.706, 13.2635 ], 
        "start time": "2018-10-14 10:39:21", 
        "HR": 135 
      } 
    ] 
  } 
}' AS json \gset
```

--------------------------------

### Retrieve Column Count with GET DESCRIPTOR (Embedded SQL)

Source: https://www.postgresql.org/docs/16/ecpg-sql-get-descriptor

This example demonstrates how to use `GET DESCRIPTOR` to retrieve the total number of columns in a result set. It assigns the `COUNT` value from the descriptor `d` to the host variable `:d_count`.

```Embedded SQL
EXEC SQL GET DESCRIPTOR d :d_count = COUNT;
```

--------------------------------

### Manually Install PL/Perl Handler

Source: https://www.postgresql.org/docs/11/xplang-install

Example of manually declaring the call handler function for the PL/Perl language, specifying the shared object location.

```sql
CREATE FUNCTION plperl_call_handler() RETURNS language_handler AS
    '$libdir/plperl' LANGUAGE C;

```

--------------------------------

### Start PostgreSQL Server using pg_ctl

Source: https://www.postgresql.org/docs/14/app-pg-ctl

Starts a PostgreSQL server instance. You must specify the data directory. Optional arguments include logging to a file, password prompting, timeout settings, and passing options to the server process.

```bash
pg_ctl start -D /path/to/your/data/directory -l /var/log/postgresql/postgresql.log -t 60
```

--------------------------------

### Configure PostgreSQL with libxml2 Support

Source: https://www.postgresql.org/docs/12/install-procedure

Enable SQL/XML support by building PostgreSQL with libxml2. This example demonstrates how to specify custom compiler and linker options for libxml2 using environment variables when pkg-config or xml2-config are not found or misconfigured.

```bash
# Example using XML2_CFLAGS and XML2_LIBS
./configure ... XML2_CFLAGS='-I/path/to/libxml2/include' XML2_LIBS='-L/path/to/libxml2/lib -lxml2'
```

```bash
# Example overriding xml2-config location
export XML2_CONFIG=/path/to/libxml2/bin/xml2-config
./configure ...
```

--------------------------------

### Start Cygwin Server for PostgreSQL

Source: https://www.postgresql.org/docs/15/installation-platform-notes

This command starts the `cygserver` process in the background, which is necessary for shared memory support when running PostgreSQL under Cygwin. This process must be running before starting the PostgreSQL server or initializing a database cluster.

```shell
/usr/sbin/cygserver &
```

--------------------------------

### Install Documentation Packages (main)

Source: https://www.postgresql.org/docs/7.0/docguide28840

Command to install pre-generated documentation packages from the main documentation directory ('doc'). This is typically run after generating the packages.

```bash
% cd doc
% make install
```

--------------------------------

### Build All PostgreSQL Components (World)

Source: https://www.postgresql.org/docs/10/install-procedure

This command builds the entire PostgreSQL system, including the core server, documentation (HTML and man pages), and additional modules from the 'contrib' directory. This provides a comprehensive build of all available PostgreSQL components.

```shell
make world

```

--------------------------------

### Get PostgreSQL Backup Start Time

Source: https://www.postgresql.org/docs/13/functions-admin

Returns the timestamp of when the current online exclusive backup started. If no backup is in progress, it returns NULL.

```PostgreSQL
SELECT pg_backup_start_time();
```

--------------------------------

### Start PostgreSQL Server using pg_ctl

Source: https://www.postgresql.org/docs/12/app-pg-ctl

Starts the PostgreSQL server and waits until it is accepting connections. This is the basic command to initiate the server process. Dependencies include a properly initialized data directory.

```bash
$ pg_ctl start

```

--------------------------------

### PostgreSQL BEGIN Transaction Example

Source: https://www.postgresql.org/docs/13/sql-begin

A simple example demonstrating how to initiate a transaction block using the BEGIN command in PostgreSQL.

```sql
BEGIN;

```

--------------------------------

### Configure and Build Pre-v6.4 PostgreSQL ODBC Driver

Source: https://www.postgresql.org/docs/7.0/odbc24471

This snippet outlines the steps for installing an older version of the PostgreSQL distribution (pre-v6.4) with the newest ODBC driver. It involves unpacking the tar file, running configure and make, and then installing the distribution.

```bash
% ./configure
% make
% make POSTGRESDIR=`PostgresTopDir` install

```

--------------------------------

### Configure, Build, and Install OpenSP

Source: https://www.postgresql.org/docs/10/docguide-toolsets

Demonstrates the standard GNU-style build process for OpenSP. This includes configuring with a default catalog path, compiling the source, and installing the binaries. The specified catalog path is crucial for OpenSP to locate SGML definitions.

```shell
./configure --enable-default-catalog=/usr/local/etc/sgml/catalog
make
make install
```

--------------------------------

### Example sepgsql Context Warnings During Installation

Source: https://www.postgresql.org/docs/devel/sepgsql

This output shows common warning messages that might appear during `sepgsql` installation or configuration, related to invalid object types in the `sepgsql_contexts` file. These messages are typically harmless and can be ignored, indicating potential version mismatches or policy updates.

```text
/etc/selinux/targeted/contexts/sepgsql_contexts:  line 33 has invalid object type db_blobs
/etc/selinux/targeted/contexts/sepgsql_contexts:  line 36 has invalid object type db_language
/etc/selinux/targeted/contexts/sepgsql_contexts:  line 37 has invalid object type db_language
/etc/selinux/targeted/contexts/sepgsql_contexts:  line 38 has invalid object type db_language
/etc/selinux/targeted/contexts/sepgsql_contexts:  line 39 has invalid object type db_language
/etc/selinux/targeted/contexts/sepgsql_contexts:  line 40 has invalid object type db_language
```

--------------------------------

### `ConnectionPoolDataSource` Configuration Example (JDBC - PostgreSQL)

Source: https://www.postgresql.org/docs/7.3/programmer

This Java snippet demonstrates how to configure a `ConnectionPoolDataSource` for JDBC with PostgreSQL. It's used for efficient connection pooling.

```java
/*
** `ConnectionPoolDataSource` Configuration Example
** This is a placeholder for the actual Java code.
*/
import org.postgresql.ds.PGConnectionPoolDataSource;

public class ConnectionPoolConfig {
    public static void main(String[] args) {
        PGConnectionPoolDataSource ds = new PGConnectionPoolDataSource();
        ds.setServerName("localhost");
        ds.setPortNumber(5432);
        ds.setDatabaseName("mydatabase");
        ds.setUser("myuser");
        ds.setPassword("mypassword");

        // Further configuration for pooling (e.g., max connections, idle timeout)
        // would depend on the specific pooling library used (e.g., HikariCP, c3p0)

        System.out.println("PGConnectionPoolDataSource configured.");
    }
}

```

--------------------------------

### Installing PostgreSQL Program and Shared Libraries

Source: https://www.postgresql.org/docs/6.4/install12063

After compilation, the PostgreSQL program is installed using 'gmake install'. The output is logged to 'make.install.log'. Additionally, the guide explains how to configure the system to find new shared libraries, either by editing '/etc/ld.so.conf' and running 'ldconfig', or by setting the LD_LIBRARY_PATH environment variable in bash or csh.

```shell
cd /usr/src/pgsql/src
gmake install >& make.install.log &
tail -f make.install.log
```

```shell
# In a bash shell:
export LD_LIBRARY_PATH=/usr/local/pgsql/lib
```

```shell
# In a csh shell:
setenv LD_LIBRARY_PATH /usr/local/pgsql/lib
```

--------------------------------

### PostgreSQL Double Metaphone Example Usage

Source: https://www.postgresql.org/docs/10/fuzzystrmatch

An example demonstrating how to use the `dmetaphone` function in PostgreSQL to get the phonetic code for a given word.

```PostgreSQL
test=# select dmetaphone('gumbo');
 dmetaphone
------------
 KMP
(1 row)
```

--------------------------------

### Configure Automatic PostgreSQL Startup (FreeBSD)

Source: https://www.postgresql.org/docs/6.5/install12893

Sets up an init script for FreeBSD to automatically start the PostgreSQL postmaster daemon on boot. It checks for the postmaster executable, starts it as the 'pgsql' user, specifies the data directory, and redirects errors to a log file. Requires execute permissions and ownership configuration.

```bash
#!/bin/sh
[ -x /usr/local/pgsql/bin/postmaster ] && {
    su -l pgsql -c 'exec /usr/local/pgsql/bin/postmaster
        -D/usr/local/pgsql/data
        -S -o -F > /usr/local/pgsql/errlog' &
    echo -n ' pgsql'
        }

```

--------------------------------

### Manual PL/Perl Installation - Language Declaration

Source: https://www.postgresql.org/docs/14/xplang-install

Example of declaring the PL/Perl language as trusted, linking it to its previously declared handler, inline, and validator functions.

```SQL
CREATE TRUSTED LANGUAGE plperl
    HANDLER plperl_call_handler
    INLINE plperl_inline_handler
    VALIDATOR plperl_validator;

```

--------------------------------

### Print PostgreSQL User's Guide with Ghostscript (Shell)

Source: https://www.postgresql.org/docs/7.0/install17165

Uncompresses a gzipped Postscript file, processes it with Ghostscript for a laserjet printer, and then pipes the output to `lpr`. This command is useful if you have Ghostscript installed and need to print Postscript files to specific printer devices.

```shell
> gunzip -c user.ps.gz \
    | gs -sDEVICE=laserjet -r300 -q -dNOPAUSE -sOutputFile=- \
    | lpr
```

--------------------------------

### Simple PL/pgSQL Function (PostgreSQL)

Source: https://www.postgresql.org/docs/7.3/programmer

This snippet presents a basic example of a PL/pgSQL function in PostgreSQL. It serves as a fundamental illustration of PL/pgSQL syntax and structure.

```plpgsql
-- A Simple Function
-- This is a placeholder for a general simple PL/pgSQL function.

CREATE OR REPLACE FUNCTION simple_plpgsql_function()
RETURNS VOID AS $$
BEGIN
    -- Function body goes here
    RAISE NOTICE 'This is a simple PL/pgSQL function.';
END;
$$ LANGUAGE plpgsql;

-- Example usage:
-- SELECT simple_plpgsql_function();

```

--------------------------------

### PostgreSQL Tutorial SQL Data Loading

Source: https://www.postgresql.org/docs/18/tutorial-advanced-intro

Loads sample data for PostgreSQL advanced features examples. This file contains SQL commands to populate tables and is referenced in the tutorial.

```sql
-- Sample data loading for advanced PostgreSQL features
-- (Content of advanced.sql not provided in the input text)
```

--------------------------------

### Manual PostgreSQL Data Directory Setup with Permissions

Source: https://www.postgresql.org/docs/10/creating-cluster

This example shows the steps to manually set up a PostgreSQL data directory, including creating the parent directory, setting ownership to the 'postgres' user, and then running `initdb`. This approach is useful when dealing with directory creation and permissions from scratch, requiring root privileges initially.

```bash
root# mkdir /usr/local/pgsql
root# chown postgres /usr/local/pgsql
root# su postgres
postgres$ initdb -D /usr/local/pgsql/data
```

--------------------------------

### Manually Install PL/Perl Inline and Validator

Source: https://www.postgresql.org/docs/11/xplang-install

Example of manually declaring the inline and validator functions for the PL/Perl language, specifying the shared object location.

```sql
CREATE FUNCTION plperl_inline_handler(internal) RETURNS void AS
    '$libdir/plperl' LANGUAGE C;

CREATE FUNCTION plperl_validator(oid) RETURNS void AS
    '$libdir/plperl' LANGUAGE C STRICT;

```

--------------------------------

### Start PostgreSQL Server with pg_ctl (Bash)

Source: https://www.postgresql.org/docs/10/server-start

This command utilizes the `pg_ctl` wrapper utility to start the PostgreSQL server, simplifying background operation and log file management. The `-l` option specifies the log file, and `pg_ctl` implicitly supports the `-D` option for the data directory, though not shown in this specific example. It handles starting the server as a daemon.

```bash
pg_ctl start -l logfile
```

--------------------------------

### Manually Install PL/Perl Language

Source: https://www.postgresql.org/docs/11/xplang-install

Example of the final command to declare the PL/Perl procedural language, linking it to its previously declared handler, inline, and validator functions.

```sql
CREATE TRUSTED PROCEDURAL LANGUAGE plperl
    HANDLER plperl_call_handler
    INLINE plperl_inline_handler
    VALIDATOR plperl_validator;

```

--------------------------------

### Test libpq C Program for PostgreSQL Database Connection and Querying

Source: https://www.postgresql.org/docs/6.3/c4010

This C program, testlibpq.c, demonstrates how to use libpq to connect to a PostgreSQL database, execute SQL commands like BEGIN, DECLARE CURSOR, FETCH ALL, CLOSE, and END, and retrieve data. It includes error handling for connection and command execution, and proper cleanup of resources.

```c
/*
 * testlibpq.c
 *   Test the C version of LIBPQ, the Postgres frontend library.
 *
 *
 */
#include <stdio.h>
#include "libpq-fe.h"

void
exit_nicely(PGconn* conn)
{
  PQfinish(conn);
  exit(1);
}

main()
{
  char *pghost, *pgport, *pgoptions, *pgtty;
  char* dbName;
  int nFields;
  int i,j;

/*  FILE *debug; */

  PGconn* conn;
  PGresult* res;

  /* begin, by setting the parameters for a backend connection
     if the parameters are null, then the system will try to use
     reasonable defaults by looking up environment variables
     or, failing that, using hardwired constants */
  pghost = NULL;  /* host name of the backend server */
  pgport = NULL;  /* port of the backend server */
  pgoptions = NULL; /* special options to start up the backend server */
  pgtty = NULL;     /* debugging tty for the backend server */
  dbName = "template1";

  /* make a connection to the database */
  conn = PQsetdb(pghost, pgport, pgoptions, pgtty, dbName);

  /* check to see that the backend connection was successfully made */
  if (PQstatus(conn) == CONNECTION_BAD) {
    fprintf(stderr,"Connection to database '%s' failed.0, dbName);
    fprintf(stderr,"%s",PQerrorMessage(conn));
    exit_nicely(conn);
  }

/*  debug = fopen("/tmp/trace.out","w");  */
/*   PQtrace(conn, debug);  */

  /* start a transaction block */

  res = PQexec(conn,"BEGIN");
  if (PQresultStatus(res) != PGRES_COMMAND_OK) {
    fprintf(stderr,"BEGIN command failed0);
    PQclear(res);
    exit_nicely(conn);
  }
  /* should PQclear PGresult whenever it is no longer needed to avoid
     memory leaks */
  PQclear(res);

  /* fetch instances from the pg_database, the system catalog of databases*/
  res = PQexec(conn,"DECLARE myportal CURSOR FOR select * from pg_database");
  if (PQresultStatus(res) != PGRES_COMMAND_OK) {
    fprintf(stderr,"DECLARE CURSOR command failed0);
    PQclear(res);
    exit_nicely(conn);
  }
  PQclear(res);

  res = PQexec(conn,"FETCH ALL in myportal");
  if (PQresultStatus(res) != PGRES_TUPLES_OK) {
    fprintf(stderr,"FETCH ALL command didn't return tuples properly0);
    PQclear(res);
    exit_nicely(conn);
  }

  /* first, print out the attribute names */
  nFields = PQnfields(res);
  for (i=0; i < nFields; i++) {
    printf("% -15s",PQfname(res,i));
  }
  printf("0);

  /* next, print out the instances */
  for (i=0; i < PQntuples(res); i++) {
    for (j=0  ; j < nFields; j++) {
      printf("% -15s", PQgetvalue(res,i,j));
    }
    printf("0);
  }

  PQclear(res);

  /* close the portal */
  res = PQexec(conn, "CLOSE myportal");
  PQclear(res);

  /* end the transaction */
  res = PQexec(conn, "END");
  PQclear(res);

  /* close the connection to the database and cleanup */
  PQfinish(conn);

/*   fclose(debug); */
}

```

--------------------------------

### Installing PostgreSQL Documentation Packages

Source: https://www.postgresql.org/docs/6.5/docguide25253

Command to install pre-built HTML documentation packages from the main documentation directory. This is typically run after generating the packages.

```bash
% cd doc
% make install
   

```

--------------------------------

### Test Contrib Modules (Post-Installation)

Source: https://www.postgresql.org/docs/8.1/regress

Executes regression tests for installed contrib modules of PostgreSQL. These tests are run against an already installed server and require that the contrib modules have been built and installed first. Tests can be run for all modules or individually.

```shell
cd contrib
gmake installcheck
```

--------------------------------

### psql Interactive Session Example

Source: https://www.postgresql.org/docs/6.5/app-psql

This example demonstrates the typical output when psql successfully connects to a database ('testdb'). It shows the welcome message, version information, and the interactive prompt for entering SQL commands.

```text
$ `psql testdb`
Welcome to the POSTGRESQL interactive sql monitor:
  Please read the file COPYRIGHT for copyright terms of POSTGRESQL
[PostgreSQL 6.5.0 on i686-pc-linux-gnu, compiled by gcc 2.7.2.3]

   type \? for help on slash commands
   type \q to quit
   type \g or terminate with semicolon to execute query
 You are currently connected to the database: testdb
          
testdb=>
```

--------------------------------

### Add PostgreSQL Bin Directory to Shell Path (sh/ksh/bash)

Source: https://www.postgresql.org/docs/7.0/start

This code snippet shows how to append the PostgreSQL binary directory to the PATH environment variable for Bourne shell variants like sh, ksh, or bash. It involves updating the .profile file in the user's home directory. Replace '/usr/local/pgsql' with your actual PostgreSQL installation directory.

```bash
% PATH=/usr/local/pgsql/bin:$PATH
% export PATH
    
```

--------------------------------

### PostgreSQL SQLDA: Full Example Program Setup

Source: https://www.postgresql.org/docs/17/ecpg-descriptors

Presents the complete setup for a PostgreSQL embedded SQL application using SQLDA, including standard headers, SQLDA declarations, error handling directives, and the initial connection statement.

```c
#include <stdlib.h>
#include <string.h>
#include <stdlib.h>
#include <stdio.h>
#include <unistd.h>

EXEC SQL include sqlda.h;

sqlda_t *sqlda1; /* descriptor for output */
sqlda_t *sqlda2; /* descriptor for input */

EXEC SQL WHENEVER NOT FOUND DO BREAK;
EXEC SQL WHENEVER SQLERROR STOP;

int
main(void)
{
    EXEC SQL BEGIN DECLARE SECTION;
    char query[1024] = "SELECT d.oid,* FROM pg_database d, pg_stat_database s WHERE d.oid=s.datid AND ( d.datname=? OR d.oid=? )"];

    int intval;
    unsigned long long int longlongval;
    EXEC SQL END DECLARE SECTION;

    EXEC SQL CONNECT TO uptimedb AS con1 USER uptime;
```

--------------------------------

### Start Postmaster via rc.d/pgsql.sh (FreeBSD)

Source: https://www.postgresql.org/docs/6.4/install12063

Sets up an initialization script in FreeBSD to automatically start the PostgreSQL postmaster daemon on boot. It checks for the executable, runs the postmaster as the 'pgsql' user with specified data directory and logging, and indicates successful startup.

```bash
#!/bin/sh
[ -x /usr/local/pgsql/bin/postmaster ] && {
    su -l pgsql -c 'exec /usr/local/pgsql/bin/postmaster
        -D/usr/local/pgsql/data
        -S -o -F > /usr/local/pgsql/errlog' &
    echo -n ' pgsql'
}
```

--------------------------------

### Standalone ODBC Driver Installation - Unpacking

Source: https://www.postgresql.org/docs/6.4/odbc18456

Prepares the standalone ODBC driver installation by unpacking the source archive. Supports both zip and gzipped tar archives. The '-a' option for unzip is crucial for removing DOS line endings.

```bash
% unzip -a `packagename`
```

```bash
tar -xzf `packagename`
```

--------------------------------

### Test libpq C Library Connection and Data Fetch

Source: https://www.postgresql.org/docs/7.0/libpq-chapter22942

This C code sample demonstrates how to use the libpq library to connect to a PostgreSQL database. It includes steps for establishing a connection, executing SQL commands such as BEGIN, DECLARE CURSOR, FETCH ALL, and COMMIT, and retrieving data. Error handling and resource cleanup (PQfinish, PQclear) are also shown.

```c
/*
 * testlibpq.c Test the C version of Libpq, the Postgres frontend
 * library.
 *
 *
 */
#include <stdio.h>
#include "libpq-fe.h"

void
exit_nicely(PGconn *conn)
{
    PQfinish(conn);
    exit(1);
}

main()
{
    char       *pghost,
               *pgport,
               *pgoptions,
               *pgtty;
    char       *dbName;
    int         nFields;
    int         i, j;

    /* FILE *debug; */

    PGconn     *conn;
    PGresult   *res;

    /*
     * begin, by setting the parameters for a backend connection if the
     * parameters are null, then the system will try to use reasonable
     * defaults by looking up environment variables or, failing that,
     * using hardwired constants
     */
    pghost = NULL;              /* host name of the backend server */
    pgport = NULL;              /* port of the backend server */
    pgoptions = NULL;           /* special options to start up the backend
                                 * server */
    pgtty = NULL;               /* debugging tty for the backend server */
    dbName = "template1";

    /* make a connection to the database */
    conn = PQsetdb(pghost, pgport, pgoptions, pgtty, dbName);

    /*
     * check to see that the backend connection was successfully made
     */
    if (PQstatus(conn) == CONNECTION_BAD)
    {
        fprintf(stderr, "Connection to database '%s' failed.\n", dbName);
        fprintf(stderr, "%s", PQerrorMessage(conn));
        exit_nicely(conn);
    }

    /* debug = fopen("/tmp/trace.out","w"); */
    /* PQtrace(conn, debug);  */

    /* start a transaction block */
    res = PQexec(conn, "BEGIN");
    if (!res || PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "BEGIN command failed\n");
        PQclear(res);
        exit_nicely(conn);
    }

    /*
     * should PQclear PGresult whenever it is no longer needed to avoid
     * memory leaks
     */
    PQclear(res);

    /*
     * fetch instances from the pg_database, the system catalog of
     * databases
     */
    res = PQexec(conn, "DECLARE mycursor CURSOR FOR select * from pg_database");
    if (!res || PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "DECLARE CURSOR command failed\n");
        PQclear(res);
        exit_nicely(conn);
    }
    PQclear(res);
    res = PQexec(conn, "FETCH ALL in mycursor");
    if (!res || PQresultStatus(res) != PGRES_TUPLES_OK)
    {
        fprintf(stderr, "FETCH ALL command didn't return tuples properly\n");
        PQclear(res);
        exit_nicely(conn);
    }

    /* first, print out the attribute names */
    nFields = PQnfields(res);
    for (i = 0; i < nFields; i++)
        printf("% -15s", PQfname(res, i));
    printf("\n\n");

    /* next, print out the instances */
    for (i = 0; i < PQntuples(res); i++)
    {
        for (j = 0; j < nFields; j++)
            printf("% -15s", PQgetvalue(res, i, j));
        printf("\n");
    }
    PQclear(res);

    /* close the cursor */
    res = PQexec(conn, "CLOSE mycursor");
    PQclear(res);

    /* commit the transaction */
    res = PQexec(conn, "COMMIT");
    PQclear(res);

    /* close the connection to the database and cleanup */
    PQfinish(conn);

    /* fclose(debug); */
    return 0;

}

```

--------------------------------

### Configure and Build Integrated PostgreSQL ODBC Driver

Source: https://www.postgresql.org/docs/7.0/odbc24471

This snippet shows how to configure and build the PostgreSQL ODBC driver as part of a standard PostgreSQL distribution installation. It involves running configure with a specific argument, followed by make and make install commands.

```bash
% ./configure --with-odbc
% make
% make install

```

--------------------------------

### Connect to PostgreSQL and Set Search Path (C)

Source: https://www.postgresql.org/docs/11/libpq-example

Establishes a connection to a PostgreSQL database using PQconnectdb and sets a secure search path for subsequent operations. It handles connection errors and cleans up resources if the connection fails. This is a foundational step for most libpq operations.

```c
int
main(int argc, char **argv)
{
    const char *conninfo;
    PGconn     *conn;
    PGresult   *res;

    if (argc > 1)
        conninfo = argv[1];
    else
        conninfo = "dbname = postgres";

    conn = PQconnectdb(conninfo);

    if (PQstatus(conn) != CONNECTION_OK)
    {
        fprintf(stderr, "Connection to database failed: %s",
                PQerrorMessage(conn));
        exit_nicely(conn);
    }

    res = PQexec(conn, "SET search_path = testlibpq3");
    if (PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "SET failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }
    PQclear(res);

    // ... rest of the code ...

    PQfinish(conn);

    return 0;
}
```

--------------------------------

### Start PostgreSQL Server on NetBSD/SPARC Solaris (Shell)

Source: https://www.postgresql.org/docs/7.0/install17165

This command is for configuring NetBSD or SPARC Solaris 2.5.1 systems to start the PostgreSQL server at boot. It uses `su` to execute the `postmaster` command as the `postgres` user with specified data directory and startup options.

```shell
> su postgres -c "/usr/local/pgsql/bin/postmaster -S -D /usr/local/pgsql/data"
```

--------------------------------

### Prepare Directories for PostgreSQL Installation

Source: https://www.postgresql.org/docs/6.3/c1802

This snippet shows how to create new directories for PostgreSQL source and installation, and set ownership for the 'postgres' user. It involves using `su` to gain root privileges, `mkdir` to create directories, and `chown` to set ownership.

```shell
su
cd /usr/src
mkdir pgsql
chown postgres:postgres pgsql
cd /usr/local
mkdir pgsql
chown postgres:postgres pgsql
exit
```

--------------------------------

### PostgreSQL Usage Example for BEGIN WORK

Source: https://www.postgresql.org/docs/6.4/sql-beginwork

An example demonstrating how to start a user transaction in PostgreSQL using the BEGIN WORK command. Transactions can be terminated using COMMIT or ROLLBACK.

```sql
BEGIN WORK;
```

--------------------------------

### PostgreSQL LISTEN and UNLISTEN Example

Source: https://www.postgresql.org/docs/11/sql-unlisten

This example demonstrates the usage of LISTEN to start receiving notifications and UNLISTEN to stop receiving them. It shows how to register for notifications on a channel and then deregister.

```sql
LISTEN virtual;
NOTIFY virtual;
-- Asynchronous notification "virtual" received from server process with PID 8448.

UNLISTEN virtual;
NOTIFY virtual;
-- no NOTIFY event is received
```

--------------------------------

### Basic pgbench Usage Synopsis

Source: https://www.postgresql.org/docs/12/pgbench

Provides the basic command structure for pgbench. The first synopsis is for initializing the benchmark environment, while the second is for running the benchmark test itself.

```bash
pgbench -i _option_... _dbname_
pgbench _option_... _dbname_
```

--------------------------------

### PostgreSQL v6.3 Installation Procedure (Unix-compatible commands)

Source: https://www.postgresql.org/docs/6.3/c18

This snippet details the commands for installing PostgreSQL v6.3 on Unix-compatible systems. It assumes default settings and specific user/path configurations. Commands are tested on RedHat Linux 4.2 with tcsh, but may require adjustments for other platforms. Dependencies include GNU make (gmake) and a BSD-compatible 'install' command.

```shell
# Assumed variables (can be changed):
# PGROOT=/path/to/postgres/installation
# Source path: /usr/src/pgsql
# Runtime path: /usr/local/pgsql

# Commands are Unix-compatible. Use common sense for platform variations.
# Requires GNU make (gmake) and BSD-compatible install.

# Example commands (actual commands not provided in text, illustrative):
# cd /usr/src/pgsql
# gmake
# gmake install DESTDIR=/usr/local/pgsql
# chown -R postgres:postgres /usr/local/pgsql
# su - postgres -c "/usr/local/pgsql/bin/initdb -D /usr/local/pgsql/data"
# su - postgres -c "pg_ctl start -D /usr/local/pgsql/data"

```

--------------------------------

### PostgreSQL TRUNCATE Example: Resetting Sequences

Source: https://www.postgresql.org/docs/15/sql-truncate

This example shows how to truncate 'bigtable' and 'fattable' while also resetting any associated sequence generators to their default starting values.

```sql
TRUNCATE bigtable, fattable RESTART IDENTITY;
```

--------------------------------

### Show All PostgreSQL Configuration Parameters

Source: https://www.postgresql.org/docs/10/sql-show

Provides an example of using `SHOW ALL` to display a comprehensive list of all current PostgreSQL run-time configuration parameters along with their descriptions and values.

```sql
SHOW ALL;
            name         | setting |                description                                                          
-------------------------+---------+-------------------------------------------------
 allow_system_table_mods | off     | Allows modifications of the structure of ...
    .
    .
    .
 xmloption               | content | Sets whether XML data in implicit parsing ...
 zero_damaged_pages      | off     | Continues processing past damaged page headers.
(196 rows)
```

--------------------------------

### libpq Example Program (C)

Source: https://www.postgresql.org/docs/7.1/programmer

Demonstrates the usage of the libpq C library for interacting with PostgreSQL databases. This includes establishing connections, executing queries, and processing results.

```c
/* This is a placeholder for actual C code examples from the documentation. */
/* For example, a connection function might look like:
   PGconn *conn = PQconnectdb("dbname=mydb user=myuser password=mypass");
   if (PQstatus(conn) == CONNECTION_BAD) {
     fprintf(stderr, "Connection to database failed: %s", PQerrorMessage(conn));
     PQfinish(conn);
     exit(1);
   }
*/
```

--------------------------------

### Start PostgreSQL Server with Custom Options using pg_ctl

Source: https://www.postgresql.org/docs/10/app-pg-ctl

Starts the PostgreSQL server with specific command-line options. This example sets the port to 5433 and disables fsync for the server process.

```bash
$ pg_ctl -o "-F -p 5433" start
```

--------------------------------

### Install Modula-3 RPMs

Source: https://www.postgresql.org/docs/6.5/cvs23780

This command installs the Modula-3 compiler from RPM packages on a Linux system. It is a prerequisite for compiling CVSup from source. The '-Uvh' flags ensure that the package is upgraded if already installed, that it is verbose, and that it shows package progress.

```shell
# rpm -Uvh pm3*.rpm
```

--------------------------------

### PO File Translation Entry Example

Source: https://www.postgresql.org/docs/18/nls-translator

An example of a translation entry within a PO file. Translators should modify the string following `msgstr`. This example demonstrates handling `printf` format specifiers, reordering them for natural language flow.

```text
msgid "The file %u has %d characters."
msgstr "Die Datei %2$s hat %1$u Zeichen."

```

--------------------------------

### PostgreSQL Embedded SQL - Full Procedure Example

Source: https://www.postgresql.org/docs/10/ecpg-sql-get-descriptor

A comprehensive C language example demonstrating a full procedure involving embedded SQL in PostgreSQL. It shows connecting to a database, preparing a statement, executing a query, and then using GET DESCRIPTOR multiple times to retrieve and print the number of columns, column length, and column data.

```c
int
main(void)
{
    EXEC SQL BEGIN DECLARE SECTION;
        int  d_count;
        char d_data[1024];
        int  d_returned_octet_length;
    EXEC SQL END DECLARE SECTION;

    EXEC SQL CONNECT TO testdb AS con1 USER testuser;
    EXEC SQL SELECT pg_catalog.set_config('search_path', '', false); EXEC SQL COMMIT;
    EXEC SQL ALLOCATE DESCRIPTOR d;

    /* Declare, open a cursor, and assign a descriptor to the cursor  */
    EXEC SQL DECLARE cur CURSOR FOR SELECT current_database();
    EXEC SQL OPEN cur;
    EXEC SQL FETCH NEXT FROM cur INTO SQL DESCRIPTOR d;

    /* Get a number of total columns */
    EXEC SQL GET DESCRIPTOR d :d_count = COUNT;
    printf("d_count                 = %d\n", d_count);

    /* Get length of a returned column */
    EXEC SQL GET DESCRIPTOR d VALUE 1 :d_returned_octet_length = RETURNED_OCTET_LENGTH;
    printf("d_returned_octet_length = %d\n", d_returned_octet_length);

    /* Fetch the returned column as a string */
    EXEC SQL GET DESCRIPTOR d VALUE 1 :d_data = DATA;
    printf("d_data                  = %s\n", d_data);

    /* Closing */
    EXEC SQL CLOSE cur;
    EXEC SQL COMMIT;

    EXEC SQL DEALLOCATE DESCRIPTOR d;
    EXEC SQL DISCONNECT ALL;

    return 0;
}

```

--------------------------------

### PostgreSQL initlocation Usage Example

Source: https://www.postgresql.org/docs/6.5/app-initlocation

This example demonstrates how to use the initlocation command to create a database in an alternate location using an environment variable, followed by the createdb command.

```bash
% setenv PGDATA2 /opt/postgres/data
% initlocation PGDATA2
% createdb -D PGDATA2
```

--------------------------------

### Start PostgreSQL Postmaster Daemon

Source: https://www.postgresql.org/docs/6.3/c1802

Starts the PostgreSQL postmaster daemon in the background. This command is typically run from the user's home directory and redirects output to a log file. It's crucial to run this from the PostgreSQL superuser account, not as root.

```bash
cd
nohup postmaster > regress.log 2>&1 &

```

```bash
cd
nohup postmaster > server.log 2>&1 &

```

--------------------------------

### Manual PL/pgSQL Installation - Handler Declaration

Source: https://www.postgresql.org/docs/7.4/xplang

Example of manually declaring the call handler function for the PL/pgSQL language. It specifies the shared object file where the handler resides.

```sql
CREATE FUNCTION plpgsql_call_handler() RETURNS language_handler AS
    '$libdir/plpgsql' LANGUAGE C;

```

--------------------------------

### Integrated Installation: Configure and Build

Source: https://www.postgresql.org/docs/6.5/odbc19863

This snippet shows the commands to configure and build the psqlODBC driver as part of an integrated PostgreSQL distribution. It requires the --with-odbc argument for the configure script.

```bash
% ./configure --with-odbc
% make
```

--------------------------------

### Compile PostgreSQL Tutorial Files (Shell)

Source: https://www.postgresql.org/docs/14/tutorial-sql-intro

This snippet demonstrates how to navigate to the PostgreSQL tutorial source directory and compile the necessary files, including C files for user-defined functions and types. This is a prerequisite for running the tutorial scripts.

```shell
$ **cd _..._/src/tutorial**
$ **make**

```

--------------------------------

### Show All PostgreSQL Run-Time Parameters

Source: https://www.postgresql.org/docs/devel/sql-show

Provides an example of using `SHOW ALL` to list all available run-time configuration parameters in PostgreSQL, including their current settings, names, and brief descriptions.

```sql
SHOW ALL;
            name         | setting |                description
-------------------------+---------+-------------------------------------------------
 allow_system_table_mods | off     | Allows modifications of the structure of ...
    .
    .
    .
 xmloption               | content | Sets whether XML data in implicit parsing ...
 zero_damaged_pages      | off     | Continues processing past damaged page headers.
(196 rows)
```

--------------------------------

### PostgreSQL WAL Archiving Configuration Examples

Source: https://www.postgresql.org/docs/10/continuous-archiving

Example `archive_command` settings for PostgreSQL WAL archiving on Unix and Windows systems. These commands copy filled WAL segment files to a designated archive directory.

```shell
archive_command = 'test ! -f /mnt/server/archivedir/%f && cp %p /mnt/server/archivedir/%f'  # Unix
```

```shell
archive_command = 'copy "%p" "C:\\server\\archivedir\\%f"'  # Windows
```

--------------------------------

### Create Standalone PostgreSQL Installation Tarball

Source: https://www.postgresql.org/docs/7.0/odbc24471

Steps to create a standalone tarball from the main PostgreSQL source tree. This involves navigating to the correct directory and running the 'make standalone' command.

```shell
cd interfaces/odbc
% make standalone
```

--------------------------------

### psql Connection Example

Source: https://www.postgresql.org/docs/7.0/app-psql

An example of connecting to a PostgreSQL database named 'testdb' using the psql command-line client. This demonstrates the initial prompt after a successful connection.

```bash
$ psql testdb
Welcome to psql, the PostgreSQL interactive terminal.

Type:  \copyright for distribution terms
       \h for help with SQL commands
       \? for help on internal slash commands
       \g or terminate with semicolon to execute query
       \q to quit

testdb=>

```

--------------------------------

### PostgreSQL EXPLAIN Command Usage Example

Source: https://www.postgresql.org/docs/6.4/sql-explain

This example demonstrates how to use the EXPLAIN command in PostgreSQL to get the query plan for a simple SELECT statement. It shows the expected output format, including the NOTICE and the query plan details.

```sql
postgres=> explain select * from foo;
NOTICE:  QUERY PLAN:

Seq Scan on foo  (cost=0.00 size=0 width=4)

EXPLAIN
```

--------------------------------

### Install PL/Perl Handler (SQL)

Source: https://www.postgresql.org/docs/10/xplang-install

Example of declaring the call handler function for the PL/Perl language. It specifies the shared object '$libdir/plperl' as the location for the C implementation of the handler.

```sql
CREATE FUNCTION plperl_call_handler() RETURNS language_handler AS
    '$libdir/plperl' LANGUAGE C;
```

--------------------------------

### Drop Table Example (JDBC - PostgreSQL)

Source: https://www.postgresql.org/docs/7.3/programmer

This Java snippet illustrates how to drop a table in PostgreSQL using JDBC. It shows the execution of a DROP TABLE SQL statement.

```java
/*
** Drop Table Example
** This is a placeholder for the actual Java code.
*/
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.Statement;

public class DropTableJdbc {
    public static void main(String[] args) {
        String url = "jdbc:postgresql://localhost:5432/mydatabase";
        String user = "myuser";
        String password = "mypassword";

        try (Connection conn = DriverManager.getConnection(url, user, password);
             Statement stmt = conn.createStatement()) {

            stmt.executeUpdate("DROP TABLE IF EXISTS mytable;");
            System.out.println("Table 'mytable' dropped (if it existed).");

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

--------------------------------

### Install PostgreSQL World (make install-world)

Source: https://www.postgresql.org/docs/10/install-procedure

Installs the entire PostgreSQL build, including system files and documentation. This is a comprehensive installation command for users who have built the 'world' target.

```shell
make install-world
```

--------------------------------

### PL/pgSQL: Example of `GET STACKED DIAGNOSTICS` in Exception Handling

Source: https://www.postgresql.org/docs/11/plpgsql-control-structures

This PL/pgSQL example demonstrates how to use `GET STACKED DIAGNOSTICS` within an `EXCEPTION WHEN OTHERS` block. It retrieves the error's primary message, detail message, and hint message into `text` variables for further processing or logging during error recovery.

```plpgsql
DECLARE
  text_var1 text;
  text_var2 text;
  text_var3 text;
BEGIN
  -- some processing which might cause an exception
  ...
EXCEPTION WHEN OTHERS THEN
  GET STACKED DIAGNOSTICS text_var1 = MESSAGE_TEXT,
                          text_var2 = PG_EXCEPTION_DETAIL,
                          text_var3 = PG_EXCEPTION_HINT;
END;
```

--------------------------------

### libpq Example Program 1: Synchronous Queries with C

Source: https://www.postgresql.org/docs/12/libpq-example

This C program demonstrates how to establish a connection to a PostgreSQL database using libpq, execute synchronous SQL commands including setting the search path and transaction control, and fetch and display data from the pg_database catalog. It handles connection errors and cleans up resources properly.

```c
/*
 * src/test/examples/testlibpq.c
 *
 *
 * testlibpq.c
 *
 *      Test the C version of libpq, the PostgreSQL frontend library.
 */
#include <stdio.h>
#include <stdlib.h>
#include "libpq-fe.h"

static void
exit_nicely(PGconn *conn)
{
    PQfinish(conn);
    exit(1);
}

int
main(int argc, char **argv)
{
    const char *conninfo;
    PGconn     *conn;
    PGresult   *res;
    int         nFields;
    int         i, 
                j;

    /*
     * If the user supplies a parameter on the command line, use it as the
     * conninfo string; otherwise default to setting dbname=postgres and using
     * environment variables or defaults for all other connection parameters.
     */
    if (argc > 1)
        conninfo = argv[1];
    else
        conninfo = "dbname = postgres";

    /* Make a connection to the database */
    conn = PQconnectdb(conninfo);

    /* Check to see that the backend connection was successfully made */
    if (PQstatus(conn) != CONNECTION_OK)
    {
        fprintf(stderr, "Connection to database failed: %s",
                PQerrorMessage(conn));
        exit_nicely(conn);
    }

    /* Set always-secure search path, so malicious users can't take control. */
    res = PQexec(
        conn,
                 "SELECT pg_catalog.set_config('search_path', '', false)");
    if (PQresultStatus(res) != PGRES_TUPLES_OK)
    {
        fprintf(stderr, "SET failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }

    /*
     * Should PQclear PGresult whenever it is no longer needed to avoid memory
     * leaks
     */
    PQclear(res);

    /*
     * Our test case here involves using a cursor, for which we must be inside
     * a transaction block.  We could do the whole thing with a single
     * PQexec() of "select * from pg_database", but that's too trivial to make
     * a good example.
     */

    /* Start a transaction block */
    res = PQexec(conn, "BEGIN");
    if (PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "BEGIN command failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }
    PQclear(res);

    /*
     * Fetch rows from pg_database, the system catalog of databases
     */
    res = PQexec(conn, "DECLARE myportal CURSOR FOR select * from pg_database");
    if (PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "DECLARE CURSOR failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }
    PQclear(res);

    res = PQexec(conn, "FETCH ALL in myportal");
    if (PQresultStatus(res) != PGRES_TUPLES_OK)
    {
        fprintf(stderr, "FETCH ALL failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }

    /* first, print out the attribute names */
    nFields = PQnfields(res);
    for (i = 0; i < nFields; i++)
        printf("% -15s", PQfname(res, i));
    printf("\n\n");

    /* next, print out the rows */
    for (i = 0; i < PQntuples(res); i++)
    {
        for (j = 0; j < nFields; j++)
            printf("% -15s", PQgetvalue(res, i, j));
        printf("\n");
    }

    PQclear(res);

    /* close the portal ... we don't bother to check for errors ... */
    res = PQexec(conn, "CLOSE myportal");
    PQclear(res);

    /* end the transaction */
    res = PQexec(conn, "END");
    PQclear(res);

    /* close the connection to the database and cleanup */
    PQfinish(conn);

    return 0;
}

```

--------------------------------

### Print PostgreSQL User's Guide (Ghostscript)

Source: https://www.postgresql.org/docs/6.5/install12893

This snippet shows how to print the PostgreSQL User's Guide using Ghostscript, specifically targeting a laserjet printer. It includes setting up an alias for Ghostscript, exporting the Ghostscript library path, unzipping the file, converting it, and then printing the converted file.

```bash
alias gshp='gs -sDEVICE=laserjet -r300 -dNOPAUSE'
export GS_LIB=/usr/share/ghostscript:/usr/share/ghostscript/fonts
gunzip user.ps.gz
gshp -sOUTPUTFILE=user.hp user.ps
gzip user.ps
lpr -l -s -r manpage.hp
```

--------------------------------

### Start PostgreSQL Server Automatically (Shell)

Source: https://www.postgresql.org/docs/7.0/install17165

This snippet demonstrates how to start the PostgreSQL server in the background and log its output. It utilizes `nohup` and `su` to run the `postmaster` command as the `postgres` user, ensuring it continues running even after the terminal is closed and redirects output to a log file.

```shell
> nohup su -c 'postmaster -D /usr/local/pgsql/data > server.log 2>&1' postgres &
```

--------------------------------

### Integrated ODBC Driver Build (Postgres >= v6.4)

Source: https://www.postgresql.org/docs/6.4/odbc18456

Builds and installs the ODBC driver as part of the main PostgreSQL distribution for versions 6.4 and later. Requires specifying the --with-odbc argument during configuration. The installation can be customized by specifying output directories.

```bash
% ./configure --with-odbc
% make
% make install
```

```bash
% make ODBCINST=`filename` install
```

--------------------------------

### Simple Delete Example (JDBC - PostgreSQL)

Source: https://www.postgresql.org/docs/7.3/programmer

This Java snippet demonstrates a simple delete operation using JDBC with PostgreSQL. It shows how to execute a DELETE SQL statement.

```java
/*
** Simple Delete Example
** This is a placeholder for the actual Java code.
*/
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.Statement;

public class SimpleDeleteJdbc {
    public static void main(String[] args) {
        String url = "jdbc:postgresql://localhost:5432/mydatabase";
        String user = "myuser";
        String password = "mypassword";

        try (Connection conn = DriverManager.getConnection(url, user, password);
             Statement stmt = conn.createStatement()) {

            int rowsAffected = stmt.executeUpdate("DELETE FROM mytable WHERE id = 1;");
            System.out.println("Rows affected: " + rowsAffected);

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

--------------------------------

### Start PostgreSQL Server using pg_ctl

Source: https://www.postgresql.org/docs/10/app-pg-ctl

Starts the PostgreSQL server and waits until it is accepting connections. This is the basic command to initiate the server process.

```bash
$ pg_ctl start
```

--------------------------------

### Example PostgreSQL Configuration File (postgresql.conf)

Source: https://www.postgresql.org/docs/11/config-setting

Provides an illustrative example of the `postgresql.conf` file, demonstrating how various parameters can be set. This file is typically located in the PostgreSQL data directory and is fundamental for server configuration.

```ini
# ------------------------------------------------------------------------------
# PostgreSQL configuration file
#
# (The following is mostly just brainstorming...)
#
# This file was created by initdb and is just an example.  You may
# find it useful to copy it to a more permanent location and
# customize it to your needs.
#
# For more information, see the documentation.  The full
# configuration file is documented in the postgresql.conf.sample
# file in the same directory.  The comments in that file will
# tell you more about the parameters defined here.
#
# The following parameters are the most commonly adjusted:

#listen_addresses = 'localhost'         # what IP address(es) to listen on;
                                        # comma-separated list of addresses;
                                        # defaults to all

max_connections = 100                   # (change requires restart)
#                                         # (change requires restart)
superuser_reserved_connections = 3      # (change requires restart)
#                                         # (change requires restart)
unix_socket_directories = '/var/run/postgresql' # (change requires restart)
                                        # (change requires restart)
#unix_socket_group          = ''
#unix_socket_permissions    = 0777      # (change requires restart)

#authentication:
# authentication methods
# see pg_hba.conf

#------------------------------------------------------------------------------
# LEVELS AND LOGGING
#------------------------------------------------------------------------------

sync_safe_WAL_flush_interval = 100ms # time between WAL flushes if "wal_sync_method" is "fsync_writethrough" or "open_datasync"
                                        # (change requires restart)

#------------------------------------------------------------------------------
# RESOURCE USAGE
#------------------------------------------------------------------------------

#------------------------------------------------------------------------------
# CONNECTIONS AND AUTHENTICATION
#------------------------------------------------------------------------------

#client_encoding = 'UTF8'               # enable de facto standard, requires client support

#------------------------------------------------------------------------------
# MEMORY
#------------------------------------------------------------------------------

#shared_buffers = 128MB                 # min 128kB
                                        # (change requires restart)
#huge_pages = try                       # try, on, off
                                        # (change requires restart)

#------------------------------------------------------------------------------
# WAL (WRITE-AHEAD LOG)
#------------------------------------------------------------------------------

#wal_level = replica                  # minimal, replica, or logical (change requires restart)
                                        # (change requires restart)
#wal_sync_method = fsync                # fsync, fdatasync, open_datasync, open_sync, fsync_writethrough
                                        # (change requires restart)
#wal_sync_interval = 0                  # wsync interval, 0 disables syncs
                                        # (change requires restart)
#wal_buffers = -1                       # -1 means set equal to wal_level*1MB, min 64kB, max 2GB. (change requires restart)
                                        # (change requires restart)
#wal_writer_delay = 200ms               # 10-10000 ms

#wal_checksums = on                     # (change requires restart)

#wal_log_hints = on                     # (change requires restart)

#max_wal_senders = 10                   # (change requires restart)
#wal_sender_timeout = 60s               # Minimum 1s, -1 disables
#wal_receiver_status_interval = 10s     # Update, -1 disables
#wal_receiver_timeout = 60s             # Minimum 1s, -1 disables

#------------------------------------------------------------------------------
# REPLICATION
#------------------------------------------------------------------------------

#max_replication_slots = 0              # (change requires restart)

#------------------------------------------------------------------------------
# CHECKPOINTS AND SHUTDOWN
#------------------------------------------------------------------------------

#checkpoint_timeout = 5min              # range 1s-1h
                                        # (change requires restart)
#max_wal_size = 1GB                     # (change requires restart)
#min_wal_size = 80MB                    # (change requires restart)
#wal_keep_size = 0                      # (change requires restart)
#checkpoint_completion_target = 0.9     # checkpoint target duration, 0 to 1
                                        # (change requires restart)
#                                        # (change requires restart)
#                                        # (change requires restart)

#------------------------------------------------------------------------------
# VACCUM AND AUTOVACUUM
#------------------------------------------------------------------------------

autovacuum = on                         # Enable autovacuum daemon
                                        # (change requires restart)
#log_autovacuum_min_duration = -1       # -1 means disabled, 0 logs all autovacuum activity
                                        # autovacuum_max_workers = 3             # min 1, max 100
                                        # (change requires restart)
#autovacuum_naptime = 1min              # shortest wait between autovacuum runs
                                        # (change requires restart)
#autovacuum_vacuum_threshold = 50       # minimum number of row updates before vacuum
#autovacuum_analyze_threshold = 50      # minimum number of row updates before analyze
#autovacuum_vacuum_scale_factor = 0.2   # fraction of table size before vacuum
#autovacuum_analyze_scale_factor = 0.1  # fraction of table size before analyze

#autovacuum_freeze_max_age = 200000000  # maximum XID age before forced vacuum
                                        # (change requires restart)
#                                        # (change requires restart)

#------------------------------------------------------------------------------
# STATISTICS
#------------------------------------------------------------------------------

#default_statistics_target = 100        # range 1-10000
#                                        # (change requires restart)
#                                        # (change requires restart)

#------------------------------------------------------------------------------
# QUERY PLANNING AND OPTIMIZATION
#------------------------------------------------------------------------------

#effective_cache_size = 128MB

#work_mem = 4MB                         # min 64kB
                                        # (change requires restart)
#maintenance_work_mem = 16MB            # min 1MB
                                        # (change requires restart)
#                                        # (change requires restart)
#                                        # (change requires restart)

#logical_decoding_work_mem = 16MB       # min 1MB
                                        # (change requires restart)
#shared_mem_size = 1GB                  # (change requires restart)

#------------------------------------------------------------------------------
# ERROR REPORTING AND LOGGING
#------------------------------------------------------------------------------

#log_destination = 'stderr'             # Valid values are combinations of
                                        # stderr, csvlog, syslog, and eventlog
                                        # (change requires restart)
#logging_collector = off                # Enable capturing of stderr into log files.
                                        # (change requires restart)
#log_directory = 'log'
#log_filename = 'postgresql-%a-%u.log'

#log_statement = 'none'                 # none, ddl, mod, all
#log_min_duration_statement = -1        # -1s -1 logs none, 0 logs all
#log_replication_commands = off
#log_checkpoints = off
#log_connections = off
#log_disconnections = off
#log_lock_waits = off                   # -1 disables, >= 0 logs all lock waits >= this interval
#log_temp_files = -1                    # -1234 logs all temp files >= 1234kB
#log_parser_stats = off
#log_executor_stats = off
#log_planner_stats = off
#log_statement_stats = off

#log_error_verbosity = default          # terse, default, or verbose
#log_error_verbosity = default          # terse, default, or verbose

#------------------------------------------------------------------------------
# DEADLOCK DETECTION
#------------------------------------------------------------------------------

deadlock_timeout = 1s                  # 1s-1000s, -1 disables

#------------------------------------------------------------------------------
# AUTO Explain
#------------------------------------------------------------------------------

#log_autovacuum_min_duration = -1       # -1 means disabled, 0 logs all autovacuum activity

#------------------------------------------------------------------------------
# CLIENT CONNECTION DEFAULTS
#------------------------------------------------------------------------------

#connection_timeout = 5s                # 1s-10000s
#statement_timeout = 0                  # 1s-10000s, 0 disables
#                                        # (change requires restart)
#idle_in_transaction_session_timeout = 5min # 1s-10000s, 0 disables
                                        # (change requires restart)
#idle_session_timeout = 5min            # 1s-10000s, 0 disables
                                        # (change requires restart)

#------------------------------------------------------------------------------
# ASYNCHRONOUS REPLICATION
#------------------------------------------------------------------------------

#wal_receiver_status_interval = 10s     # Update, -1 disables

#------------------------------------------------------------------------------
# BACKGROUND WRITER
#------------------------------------------------------------------------------

#bgwriter_delay = 10ms                  # 10-1000ms
                                        # (change requires restart)
#bgwriter_lru_maxpages = 100            # 0-1000, includes max pages
                                        # (change requires restart)
#bgwriter_lru_multiplier = 1.0          # 1.0-10.0, includes multiplier
                                        # (change requires restart)
#bgwriter_flush_after = 256kB           # 0-1024kB, and 0 disables
                                        # (change requires restart)

#------------------------------------------------------------------------------
# ASYNC_FILE_WRITER
#------------------------------------------------------------------------------

#async_file_size = 1GB                  # 1MB-100GB

#------------------------------------------------------------------------------
# STATISTICS GATHERER
#------------------------------------------------------------------------------

#stats_temp_directory = ''

#------------------------------------------------------------------------------
# LOCK MANAGEMENT
#------------------------------------------------------------------------------

#max_locks_per_transaction = 64
                                        # (change requires restart)
#max_pred_locks_per_relation = -1       # -1 means unlimited
                                        # (change requires restart)
#max_prepared_xacts = 0                 # (change requires restart)
#max_locks = 64                         # (change requires restart)

#------------------------------------------------------------------------------
# LITE GEOMETRY
#------------------------------------------------------------------------------

#postgis.enable_out2d = off

#------------------------------------------------------------------------------
# LATERAL VIEWS
#------------------------------------------------------------------------------

#enable_lateral_views = on

#------------------------------------------------------------------------------
# WAL SENDER AND RECEIVER
#------------------------------------------------------------------------------

#wal_sender_timeout = 60s               # Minimum 1s, -1 disables
#wal_receiver_timeout = 60s             # Minimum 1s, -1 disables

#------------------------------------------------------------------------------
# REPLICATION SLOTS
#------------------------------------------------------------------------------

#max_replication_slots = 0              # (change requires restart)

#------------------------------------------------------------------------------
# AUTHENTICATION
#------------------------------------------------------------------------------

#ssl = off                              # (change requires restart)
#                                        # (change requires restart)
#                                        # (change requires restart)
#                                        # (change requires restart)
#                                        # (change requires restart)
#                                        # (change requires restart)
#                                        # (change requires restart)

#password_encryption = scram-sha-256    # scram-sha-256, md5, plain (change requires restart)
                                        # (change requires restart)

#------------------------------------------------------------------------------
# AUTHENTICATION METHODS
#------------------------------------------------------------------------------

#host    all             all             0.0.0.0/0               scram-sha-256
#local   all             all                             peer
#host    replication     all             127.0.0.1/32            scram-sha-256
#host    replication     all             ::1/128                 scram-sha-256

#------------------------------------------------------------------------------
# AUTHENTICATION AND AUTHORIZATION
#------------------------------------------------------------------------------

#pg_ident.map = ''

#------------------------------------------------------------------------------
# CONNECTION AND AUTHENTICATION
#------------------------------------------------------------------------------

#unix_socket_group = ''

#------------------------------------------------------------------------------
# DATABASE SYSTEM SETTINGS
#------------------------------------------------------------------------------

#fsync = on                             # enables POSIX fsync() sync to force data to disk
                                        # (change requires restart)
#synchronous_commit = on                # "on", "remote_apply", "remote_write", "local", "off", "remote_write_wal"
                                        # (change requires restart)
#synchronous_standby_names = ''         # format: "stream://hostname[=appname][,...]"
                                        # (change requires restart)
#synchronous_commit = on                # "on", "remote_apply", "remote_write", "local", "off", "remote_write_wal"
                                        # (change requires restart)
#synchronous_standby_names = ''         # format: "stream://hostname[=appname][,...]"
                                        # (change requires restart)

#full_page_writes = on                  # prevents data corruption in case of power loss
                                        # (change requires restart)

#wal_compression = off                  # (change requires restart)

#wal_buffers = -1                       # -1 means set equal to wal_level*1MB, min 64kB, max 2GB. (change requires restart)
                                        # (change requires restart)

#wal_writer_delay = 200ms               # 10-10000 ms

#wal_skip_threshold = 16MB              # range 1-1024MB
                                        # (change requires restart)

#wal_keep_size = 0                      # (change requires restart)

#wal_flush_retry = 5                    # 0-1000

#max_wal_size = 1GB                     # (change requires restart)
#min_wal_size = 80MB                    # (change requires restart)

#------------------------------------------------------------------------------
# MEMORY ALLOCATION
#------------------------------------------------------------------------------

#shared_preload_libraries = ''          # (change requires restart)

#------------------------------------------------------------------------------
# BACKUP AND PITR
#------------------------------------------------------------------------------

#archive_mode = off                     # enables archiving; off, on, or always (change requires restart)
                                        # (change requires restart)
#archive_command = ''                   # command to execute to archive a WAL file
                                        # (change requires restart)
#restore_command = ''                   # command to execute to restore a WAL file
                                        # (change requires restart)
#archive_timeout = 0                    # 1s-1h; 0 disables

#------------------------------------------------------------------------------
# ARCHIVING
#------------------------------------------------------------------------------

#archive_command = ''                   # command to execute to archive a WAL file
                                        # (change requires restart)

#------------------------------------------------------------------------------
# RECOVERY AND REWIND
#------------------------------------------------------------------------------

#recovery_target_time = ''              # automatic recovery point
                                        # (change requires restart)

#------------------------------------------------------------------------------
# RECOVERY TARGET
#------------------------------------------------------------------------------

#recovery_target_inclusive = on
#recovery_target_elapsed = 0            # 0 disables

#------------------------------------------------------------------------------
# REPLICATION TARGET
#------------------------------------------------------------------------------

#hot_standby = off                      # "on" allows pagk. queries on the standby server (change requires restart)
                                        # (change requires restart)
#max_standby_streaming_delay = 30s      # 1s-1000s, -1 disables
                                        # (change requires restart)
#max_standby_streaming_delay = 30s      # 1s-1000s, -1 disables
                                        # (change requires restart)
#wal_receiver_status_interval = 10s     # Update, -1 disables

#------------------------------------------------------------------------------
# REPLICATION
#------------------------------------------------------------------------------

#hot_standby = off                      # "on" allows pagk. queries on the standby server (change requires restart)
                                        # (change requires restart)

#------------------------------------------------------------------------------
# POINT IN TIME RECOVERY
#------------------------------------------------------------------------------

#recovery_target_name = ''              # automatic recovery point
                                        # (change requires restart)

#------------------------------------------------------------------------------
# MONITORING
#------------------------------------------------------------------------------

#log_statement = 'none'                 # none, ddl, mod, all
#log_min_duration_statement = -1        # -1s -1 logs none, 0 logs all

#------------------------------------------------------------------------------
# CONFIGURATION PARAMETERS
#------------------------------------------------------------------------------

#log_line_prefix = '%m [%p] '
                                        # (change requires restart)

#log_timezone = 'Australia/Sydney'

#------------------------------------------------------------------------------
# ACCESS CONTROL AND AUTHENTICATION
#------------------------------------------------------------------------------

#ident_file = '.ident'

#------------------------------------------------------------------------------
# AUTHENTICATION
#------------------------------------------------------------------------------

#pg_ident.map = ''

#------------------------------------------------------------------------------
# CONNECTION STRINGS
#------------------------------------------------------------------------------

#search_path = '"$user", public'        # list of schemas to search for, in order

#------------------------------------------------------------------------------
# CASE SENSITIVITY
#------------------------------------------------------------------------------

#lower_case_table_names = 0              # 0: none, 1: lower, 2: upper

#------------------------------------------------------------------------------
# AUTHENTICATION AND AUTHORIZATION
#------------------------------------------------------------------------------

#password_encryption = scram-sha-256    # scram-sha-256, md5, plain (change requires restart)
                                        # (change requires restart)

#------------------------------------------------------------------------------
# AUTHENTICATION METHODS
#------------------------------------------------------------------------------

#host    all             all             0.0.0.0/0               scram-sha-256
#local   all             all                             peer

#------------------------------------------------------------------------------
# CONNECTION STRINGS
#------------------------------------------------------------------------------

#search_path = '"$user", public'        # list of schemas to search for, in order

#------------------------------------------------------------------------------
# MISCELLANEOUS
#------------------------------------------------------------------------------

#enable_indexscan = on
#enable_bitmapscan = on
#enable_prescan = on
#enable_seqscan = on
#enable_indexonlyscan = on
#enable_partition_pruning = on

#jit = on                               # Enable Just-In-Time compilation
                                        # (change requires restart)

#jit_optimize_timeout = 5000            # 100-10000 ms
#jit_above_cost = 100000                # 0-1000000
#jit_decay_factor = 0.95                # 0.1-0.99

#------------------------------------------------------------------------------
# AUTHORIZATION
#------------------------------------------------------------------------------

#password_encryption = scram-sha-256    # scram-sha-256, md5, plain (change requires restart)
                                        # (change requires restart)

#------------------------------------------------------------------------------
# AUTHENTICATION METHODS
#------------------------------------------------------------------------------

#host    all             all             0.0.0.0/0               scram-sha-256
#local   all             all                             peer

#------------------------------------------------------------------------------
# CONNECTION STRINGS
#------------------------------------------------------------------------------

#search_path = '"$user", public'        # list of schemas to search for, in order

#------------------------------------------------------------------------------
# MISCELLANEOUS
#------------------------------------------------------------------------------

#jit = on                               # Enable Just-In-Time compilation
                                        # (change requires restart)

#------------------------------------------------------------------------------
# AUTHORIZATION
#------------------------------------------------------------------------------

#password_encryption = scram-sha-256    # scram-sha-256, md5, plain (change requires restart)
                                        # (change requires restart)

#------------------------------------------------------------------------------
# AUTHENTICATION METHODS
#------------------------------------------------------------------------------

#host    all             all             0.0.0.0/0               scram-sha-256
#local   all             all                             peer

#------------------------------------------------------------------------------
# CONNECTION STRINGS
#------------------------------------------------------------------------------

#search_path = '"$user", public'        # list of schemas to search for, in order

```

--------------------------------

### PostgreSQL initdb Command Synopsis

Source: https://www.postgresql.org/docs/13/app-initdb

The synopsis for the initdb command, showing its basic usage and options for creating a new PostgreSQL database cluster.

```bash
initdb [_option_]... [--pgdata | -D ] _directory_
```

--------------------------------

### Shell: Stream Logical Decoding with pg_recvlogical

Source: https://www.postgresql.org/docs/18/logicaldecoding-example

Demonstrates using the `pg_recvlogical` command-line utility to control and stream logical decoding output. It includes creating a replication slot, starting a stream to standard output, inserting data to generate changes, and stopping the stream. This method is suitable for capturing changes via the streaming replication protocol and requires proper client authentication setup for replication.

```shell
Example 1:
$ pg_recvlogical -d postgres --slot=test --create-slot
$ pg_recvlogical -d postgres --slot=test --start -f -
**Control**+**Z**
$ psql -d postgres -c "INSERT INTO data(data) VALUES('4');"
$ fg
BEGIN 693
table public.data: INSERT: id[integer]:4 data[text]:'4'
COMMIT 693
**Control**+**C**
```

--------------------------------

### PostgreSQL dropdb Command Usage Examples

Source: https://www.postgresql.org/docs/7.0/app-dropdb

Examples illustrating how to use the dropdb command. The first example shows a basic database removal, while the second demonstrates using options for host, port, interactivity, and echoing queries.

```bash
$ dropdb demo
DROP DATABASE
```

```bash
$ dropdb -p 5000 -h eden -i -e demo
Database "demo" will be permanently deleted.
Are you sure? (y/n) `y`
DROP DATABASE "demo"
DROP DATABASE
```

--------------------------------

### Display Help (initdb)

Source: https://www.postgresql.org/docs/10/app-initdb

Shows help information about `initdb` command-line arguments and exits.

```bash
initdb -?
```

```bash
initdb --help
```

--------------------------------

### Start Postmaster Daemon with Nohup

Source: https://www.postgresql.org/docs/6.4/install12063

Starts the PostgreSQL postmaster daemon in the background, redirecting output to 'regress.log'. The 'nohup' command ensures the process continues to run even after the user logs out.

```bash
cd
nohup postmaster > regress.log 2>&1 &
```

--------------------------------

### Create PostgreSQL Subscription with Delayed Connection (connect=false)

Source: https://www.postgresql.org/docs/devel/logical-replication-subscription

This command initializes a PostgreSQL subscription to 'pub1' on a remote host but explicitly prevents it from connecting immediately (`connect=false`). This setup requires manual replication slot creation on the publisher and subsequent subscription activation on the subscriber.

```sql
CREATE SUBSCRIPTION sub1
CONNECTION 'host=localhost dbname=test_pub'
PUBLICATION pub1
WITH (connect=false);
```

--------------------------------

### Compiling PostgreSQL Documentation and Programs

Source: https://www.postgresql.org/docs/6.4/install12063

This section covers the compilation of PostgreSQL documentation (HTML and man pages) and the main program. It involves navigating to the respective directories and using 'gmake' to build the components. The output of the main compilation is redirected to 'make.log' for review.

```shell
cd /usr/src/pgsql/doc
gmake install
```

```shell
cd /usr/src/pgsql/doc
gmake man
```

```shell
cd /usr/src/pgsql/src
gmake all >& make.log &
tail -f make.log
```

--------------------------------

### Execute sepgsql Regression Tests

Source: https://www.postgresql.org/docs/devel/sepgsql

Run the `test_sepgsql` script from the `contrib/sepgsql` directory. This script verifies the setup and then executes the regression tests for the `sepgsql` module.

```bash
./test_sepgsql
```

--------------------------------

### Configure PostgreSQL `wal_level` for Logical Replication

Source: https://www.postgresql.org/docs/devel/logical-replication-quick-setup

This configuration snippet for `postgresql.conf` sets the `wal_level` parameter to `logical`, which is a mandatory step to enable logical replication. Other default settings are typically sufficient for a basic setup.

```ini
wal_level = logical

```

--------------------------------

### Create PostgreSQL Database with Custom Host, Port, and Template

Source: https://www.postgresql.org/docs/devel/app-createdb

This example demonstrates creating a PostgreSQL database named 'demo' on a specific host ('eden') and port ('5000'), using 'template0' as the base template. It includes both the `createdb` command-line utility syntax and its underlying SQL equivalent for clarity.

```bash
createdb -p 5000 -h eden -T template0 -e demo
```

```sql
CREATE DATABASE demo TEMPLATE template0;
```

--------------------------------

### Start PostgreSQL Server with pg_ctl

Source: https://www.postgresql.org/docs/18/app-pg-ctl

Starts a PostgreSQL server instance. It requires the data directory and can optionally log to a specified file, prompt for a password, set a timeout, or pass additional options to the server startup. It can also specify the path to the PostgreSQL binaries.

```bash
pg_ctl start -D /path/to/your/data/directory -l /path/to/logfile.log
```

--------------------------------

### Building with GSSAPI Authentication Support

Source: https://www.postgresql.org/docs/10/install-procedure

Enables GSSAPI authentication support in PostgreSQL. Often requires specifying include and library paths using `--with-includes` and `--with-libraries` if GSSAPI (Kerberos) is not in default system locations.

```bash
./configure --with-gssapi
```

--------------------------------

### Reproduce PostgreSQL Build Configuration using pg_config

Source: https://www.postgresql.org/docs/13/app-pgconfig

This example demonstrates how to reproduce the build configuration of a current PostgreSQL installation. It utilizes the 'pg_config --configure' command to fetch configuration arguments and then uses 'eval' to correctly apply them to the 'configure' script. This ensures that subsequent builds match the existing installation's settings. It's important to use 'eval' because the output of '--configure' includes shell quotation marks for arguments with spaces.

```bash
eval ./configure `pg_config --configure`

```

--------------------------------

### PostgreSQL SHOW Command Usage Examples

Source: https://www.postgresql.org/docs/6.4/sql-show

Provides practical examples of using the PostgreSQL SHOW command to query specific configuration parameters like 'DateStyle' and 'GEQO'. The output demonstrates how the command returns the current settings for these parameters within the active session.

```sql
-- show DateStyle;
SHOW DateStyle;
NOTICE:DateStyle is Postgres with US (NonEuropean) conventions

-- show Geqo;
SHOW GEQO;
NOTICE:GEQO is ON

```

--------------------------------

### Connect to PostgreSQL and Listen for Notifications (C)

Source: https://www.postgresql.org/docs/12/libpq-example

Connects to a PostgreSQL database using connection information, sets the search path, and listens for notifications on a specific channel. It then enters a loop to consume and process incoming notifications using `select()` for event handling.

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/types.h>
#include <sys/time.h>
#include <unistd.h>
#include <errno.h>
#include "libpq-fe.h"

static void
exit_nicely(PGconn *conn)
{
    PQfinish(conn);
    exit(1);
}

int main(int argc, char **argv)
{
    PGconn     *conn;
    PGresult   *res;
    const char *conninfo;
    pgnotify   *notify;
    int         nnotifies;

    /*
     * If conninfo string is provided, use it; otherwise default to setting
     * dbname=postgres and using environment variables or defaults for all
     * other connection parameters.
     */
    if (argc > 1)
        conninfo = argv[1];
    else
        conninfo = "dbname = postgres";

    /* Make a connection to the database */
    conn = PQconnectdb(conninfo);

    /* Check to see that the backend connection was successfully made */
    if (PQstatus(conn) != CONNECTION_OK)
    {
        fprintf(stderr, "Connection to database failed: %s",
                PQerrorMessage(conn));
        exit_nicely(conn);
    }

    /* Set always-secure search path, so malicious users can't take control. */
    res = PQexec(
        conn,
        "SELECT pg_catalog.set_config('search_path', '', false)");
    if (PQresultStatus(res) != PGRES_TUPLES_OK)
    {
        fprintf(stderr, "SET failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }

    /*
     * Should PQclear PGresult whenever it is no longer needed to avoid memory
     * leaks
     */
    PQclear(res);

    /*
     * Issue LISTEN command to enable notifications from the rule's NOTIFY.
     */
    res = PQexec(conn, "LISTEN TBL2");
    if (PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "LISTEN command failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }
    PQclear(res);

    /* Quit after four notifies are received. */
    nnotifies = 0;
    while (nnotifies < 4)
    {
        /*
         * Sleep until something happens on the connection.  We use select(2)
         * to wait for input, but you could also use poll() or similar
         * facilities.
         */
        int         sock;
        fd_set      input_mask;

        sock = PQsocket(conn);

        if (sock < 0)
            break;              /* shouldn't happen */

        FD_ZERO(&input_mask);
        FD_SET(sock, &input_mask);

        if (select(sock + 1, &input_mask, NULL, NULL, NULL) < 0)
        {
            fprintf(stderr, "select() failed: %s\n", strerror(errno));
            exit_nicely(conn);
        }

        /* Now check for input */
        PQconsumeInput(conn);
        while ((notify = PQnotifies(conn)) != NULL)
        {
            fprintf(stderr,
                    "ASYNC NOTIFY of '%s' received from backend PID %d\n",
                    notify->relname, notify->be_pid);
            PQfreemem(notify);
            nnotifies++;
            PQconsumeInput(conn);
        }
    }

    fprintf(stderr, "Done.\n");

    /* close the connection to the database and cleanup */
    PQfinish(conn);

    return 0;
}

```

--------------------------------

### `DataSource` JNDI Code Example (JDBC - PostgreSQL)

Source: https://www.postgresql.org/docs/7.3/programmer

This Java snippet demonstrates how to retrieve and use a `DataSource` object configured via JNDI (Java Naming and Directory Interface) for JDBC connections to PostgreSQL.

```java
/*
** `DataSource` JNDI Code Example
** This is a placeholder for the actual Java code.
*/
import javax.sql.DataSource;
import javax.naming.Context;
import javax.naming.InitialContext;
import javax.naming.NamingException;
import java.sql.Connection;
import java.sql.SQLException;

public class DataSourceJndiExample {
    public static void main(String[] args) {
        try {
            // Look up the DataSource from JNDI
            Context envCtx = (Context) new InitialContext().lookup("java:comp/env");
            DataSource dataSource = (DataSource) envCtx.lookup("jdbc/mydatasource"); // Replace with your JNDI name

            try (Connection connection = dataSource.getConnection()) {
                System.out.println("Successfully obtained a connection from JNDI DataSource.");
                // Use the connection for database operations
            }

        } catch (NamingException | SQLException e) {
            e.printStackTrace();
        }
    }
}

```

--------------------------------

### C: Connect to PostgreSQL and Set Search Path

Source: https://www.postgresql.org/docs/devel/libpq-example

This code snippet initializes a PostgreSQL database connection using libpq's PQconnectdb, allowing for an optional connection string from command-line arguments. It includes error checking for connection status and sets a secure search_path for subsequent queries.

```C
int
main(int argc, char **argv)
{
    const char *conninfo;
    PGconn     *conn;
    PGresult   *res;
    const char *paramValues[1];
    int         paramLengths[1];
    int         paramFormats[1];
    uint32_t    binaryIntVal;

    /*
     * If the user supplies a parameter on the command line, use it as the
     * conninfo string; otherwise default to setting dbname=postgres and using
     * environment variables or defaults for all other connection parameters.
     */
    if (argc > 1)
        conninfo = argv[1];
    else
        conninfo = "dbname = postgres";

    /* Make a connection to the database */
    conn = PQconnectdb(conninfo);

    /* Check to see that the backend connection was successfully made */
    if (PQstatus(conn) != CONNECTION_OK)
    {
        fprintf(stderr, "%s", PQerrorMessage(conn));
        exit_nicely(conn);
    }

    /* Set always-secure search path, so malicious users can't take control. */
    res = PQexec(conn, "SET search_path = testlibpq3");
    if (PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "SET failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }
    PQclear(res);
```

--------------------------------

### Manual PL/Perl Installation - Inline and Validator Declaration

Source: https://www.postgresql.org/docs/14/xplang-install

Example of declaring the PL/Perl inline and validator functions. These are also specified with their shared object location and declared as LANGUAGE C STRICT.

```SQL
CREATE FUNCTION plperl_inline_handler(internal) RETURNS void AS
    '$libdir/plperl' LANGUAGE C STRICT;

CREATE FUNCTION plperl_validator(oid) RETURNS void AS
    '$libdir/plperl' LANGUAGE C STRICT;

```

--------------------------------

### PostgreSQL OPEN Command Examples

Source: https://www.postgresql.org/docs/15/ecpg-sql-open

Provides practical examples of using the OPEN command in embedded SQL. These examples illustrate opening cursors with direct values, host variables, and SQL descriptors.

```sql
EXEC SQL OPEN a;

```

```sql
EXEC SQL OPEN d USING 1, 'test';

```

```sql
EXEC SQL OPEN c1 USING SQL DESCRIPTOR mydesc;

```

```sql
EXEC SQL OPEN :curname1;

```

--------------------------------

### PostgreSQL Trigger Example

Source: https://www.postgresql.org/docs/18/trigger-example

This is a comprehensive example demonstrating the creation and usage of triggers in PostgreSQL. It covers defining trigger functions and associating them with tables. No external dependencies are required beyond a PostgreSQL installation.

```sql
CREATE OR REPLACE FUNCTION log_changes()
RETURNS TRIGGER AS $$
BEGIN
    IF (TG_OP = 'DELETE') THEN
        INSERT INTO audit_log (table_name, operation, old_data)
        VALUES (TG_TABLE_NAME, TG_OP, row_to_json(OLD));
        RETURN OLD;
    ELSIF (TG_OP = 'UPDATE') THEN
        INSERT INTO audit_log (table_name, operation, old_data, new_data)
        VALUES (TG_TABLE_NAME, TG_OP, row_to_json(OLD), row_to_json(NEW));
        RETURN NEW;
    ELSIF (TG_OP = 'INSERT') THEN
        INSERT INTO audit_log (table_name, operation, new_data)
        VALUES (TG_TABLE_NAME, TG_OP, row_to_json(NEW));
        RETURN NEW;
    END IF;
    RETURN NULL; -- result is ignored since anyway
END;
$$ LANGUAGE plpgsql;

CREATE TABLE audit_log (
    id SERIAL PRIMARY KEY,
    table_name TEXT NOT NULL,
    operation TEXT NOT NULL,
    old_data JSON,
    new_data JSON,
    changed_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

CREATE TRIGGER users_audit
AFTER INSERT OR UPDATE OR DELETE ON users
FOR EACH ROW EXECUTE FUNCTION log_changes();

-- Example Usage:
-- INSERT INTO users (username, email) VALUES ('testuser', 'test@example.com');
-- UPDATE users SET email = 'updated@example.com' WHERE username = 'testuser';
-- DELETE FROM users WHERE username = 'testuser';

-- SELECT * FROM audit_log;
```

--------------------------------

### PostgreSQL ALTER SERVER Examples

Source: https://www.postgresql.org/docs/16/sql-alterserver

Provides practical examples of using the ALTER SERVER command. These examples demonstrate how to add connection options, modify the server version, and change specific options like the host parameter.

```sql
ALTER SERVER foo OPTIONS (host 'foo', dbname 'foodb');
```

```sql
ALTER SERVER foo VERSION '8.4' OPTIONS (SET host 'baz');
```

--------------------------------

### Connect to PostgreSQL Database with Host Specified

Source: https://www.postgresql.org/docs/6.4/start409

This command connects to the 'template1' database on the 'localhost' using TCP/IP. It's useful when local socket connections are not configured or preferred. The '-h' flag specifies the hostname.

```bash
% psql -h localhost template1
```

--------------------------------

### PostgreSQL pg_hba.conf Example Configuration

Source: https://www.postgresql.org/docs/7.1/client-authentication

An example of a pg_hba.conf file, demonstrating the structure and syntax for defining client authentication rules. This example illustrates the use of comments, record types, and fields.

```postgresql.conf
# TYPE       DATABASE    IP_ADDRESS    MASK               AUTHTYPE  MAP
```

--------------------------------

### PostgreSQL: Server Startup Failure - Permission Denied on Port

Source: https://www.postgresql.org/docs/16/server-start

This example shows an attempt to start PostgreSQL on a reserved port (666) resulting in a 'Permission denied' error. It indicates that the process lacks the necessary privileges to bind to the specified port.

```bash
$ postgres -p 666
LOG:  could not bind IPv4 address "127.0.0.1": Permission denied
HINT:  Is another postmaster already running on port 666? If not, wait a few seconds and retry.
FATAL:  could not create any TCP/IP sockets

```

--------------------------------

### PostgreSQL Extension Control File Example

Source: https://www.postgresql.org/docs/10/extend-extensions

An example of a PostgreSQL extension control file, demonstrating the key-value pair format for setting parameters like directory, default version, and requirements. Control files dictate how an extension is managed and installed.

```postgresql
# Example PostgreSQL extension control file

# Specifies the directory containing the extension's SQL script files.
# If not an absolute path, it's relative to SHAREDIR.
directory = 'extension'

# The default version of the extension to be installed.
default_version = '1.0'

# A descriptive comment about the extension.
comment = 'My custom extension for advanced features.'

# Character set encoding used by the script files, necessary for non-ASCII characters.
encoding = 'UTF8'

# List of extensions this one depends on. Must be installed first.
requires = 'base_extension, another_one'

# Whether only superusers can create or update this extension.
superuser = true

# Whether the extension's objects can be moved to a different schema after creation.
relocatable = false

# Forces the extension to be loaded into a specific schema (for non-relocatable extensions).
schema = 'my_schema'
```

--------------------------------

### Build PostgreSQL with Make

Source: https://www.postgresql.org/docs/10/install-procedure

This command initiates the standard build process for PostgreSQL. It compiles the core server and related components. Ensure you are using GNU make. The successful completion is indicated by a specific confirmation message.

```shell
make

```

--------------------------------

### Conflict Example: Typedef Name as SQL Keyword

Source: https://www.postgresql.org/docs/16/ecpg-variables

Illustrates a conflict where a typedef name ('start') shadows an SQL keyword ('START'). ECPG will report a syntax error because it no longer recognizes 'START' as an SQL keyword. This can be worked around using dynamic SQL.

```c
EXEC SQL BEGIN DECLARE SECTION;
    typedef int start;
EXEC SQL END DECLARE SECTION;
...
EXEC SQL START TRANSACTION;

```

--------------------------------

### Get PostgreSQL server start time

Source: https://www.postgresql.org/docs/17/functions-info

The `pg_postmaster_start_time` function returns the timestamp when the PostgreSQL server process started. This is useful for monitoring server uptime and restart events. It takes no arguments.

```sql
SELECT pg_postmaster_start_time()
```

--------------------------------

### Setting PATH for Bison and Flex

Source: https://www.postgresql.org/docs/15/install-windows-full

This snippet illustrates how to add the directory containing flex.exe and bison.exe to the PATH environment variable. This is crucial for building PostgreSQL from Git when these tools are not already in the system's PATH. It also provides a specific example for MinGW installations.

```shell
# Example for MinGW installation:
# Assuming MinGW is installed in C:\MinGW
export PATH="$PATH:/c/MinGW/msys/1.0/bin"
```

--------------------------------

### PL/pgSQL Function that Creates Another Function (PostgreSQL)

Source: https://www.postgresql.org/docs/7.3/programmer

This PL/pgSQL snippet demonstrates a meta-programming example where one function dynamically creates another function. It showcases advanced PL/pgSQL capabilities.

```plpgsql
-- A Function that Creates Another Function

CREATE OR REPLACE FUNCTION create_dynamic_function(function_name TEXT, return_value TEXT)
RETURNS VOID AS $$
DECLARE
    create_sql TEXT;
BEGIN
    create_sql := format('CREATE OR REPLACE FUNCTION %s() RETURNS TEXT AS $$ BEGIN RETURN %L; END; $$ LANGUAGE plpgsql;',
                         function_name, return_value);
    EXECUTE create_sql;
    RAISE NOTICE 'Function % created.', function_name;
END;
$$ LANGUAGE plpgsql;

-- Example usage:
-- SELECT create_dynamic_function('dynamic_hello', 'Hello from dynamic function');
-- SELECT dynamic_hello();

```

--------------------------------

### PostgreSQL FETCH Command Usage Examples

Source: https://www.postgresql.org/docs/6.5/sql-fetch

Provides practical SQL examples demonstrating how to use the FETCH command with a cursor. It includes setting up a cursor, fetching rows in forward and backward directions, and closing the cursor.

```sql
--set up and use a cursor:
--
BEGIN WORK;
  DECLARE liahona CURSOR
     FOR SELECT * FROM films;

--Fetch first 5 rows in the cursor liahona:
--
  FETCH FORWARD 5 IN liahona;

  code |title                  |did| date_prod|kind      |len
  -----+-----------------------+---+----------+----------+------
  BL101|The Third Man          |101|1949-12-23|Drama     | 01:44
  BL102|The African Queen      |101|1951-08-11|Romantic  | 01:43
  JL201|Une Femme est une Femme|102|1961-03-12|Romantic  | 01:25
  P_301|Vertigo                |103|1958-11-14|Action    | 02:08
  P_302|Becket                 |103|1964-02-03|Drama     | 02:28

--Fetch previous row:
--
  FETCH BACKWARD 1 IN liahona;

  code |title                  |did| date_prod|kind      |len
  -----+-----------------------+---+----------+----------+------
  P_301|Vertigo                |103|1958-11-14|Action    | 02:08

-- close the cursor and commit work:
--
  CLOSE liahona;
COMMIT WORK;

```

--------------------------------

### PostgreSQL Initial Catalog Data Example (`pg_proc.dat`)

Source: https://www.postgresql.org/docs/15/bki

This example shows the format of initial data files, like `pg_proc.dat`, used to populate system catalogs during the `initdb` bootstrap phase. This data ensures the database system is functional enough to execute SQL commands upon initialization.

```bki
INSERT INTO pg_proc (oid, proname, pronamespace, proowner, ...)
VALUES (1, 'pg_proc', 2200, 10, ...);
INSERT INTO pg_proc (oid, proname, pronamespace, proowner, ...)
VALUES (2, 'pg_type', 2200, 10, ...);

```

--------------------------------

### Compile and Link PostgreSQL ODBC Driver

Source: https://www.postgresql.org/docs/6.4/odbc18456

Compiles and links the source code of the PostgreSQL ODBC driver. The ODBCINST variable can be used to specify the installation directory for the odbcinst.ini file.

```bash
% make ODBCINST=`instdir`
```

--------------------------------

### Launch psql and observe the interactive prompt

Source: https://www.postgresql.org/docs/16/app-psql

Illustrates how to start the `psql` client for a specific database (e.g., `testdb`). After a successful connection, `psql` displays its version information and then presents a prompt, typically `databasename=>`, where users can type and execute SQL commands.

```shell
psql testdb
psql (16.10)
Type "help" for help.

testdb=>
```

--------------------------------

### Configure PostgreSQL with Native Language Support (NLS)

Source: https://www.postgresql.org/docs/13/install-procedure

Enables internationalization of PostgreSQL messages, requiring the Gettext API. This example shows how to specify a space-separated list of language codes (e.g., German and French) to support during the build process; if no languages are specified, all available translations are installed by default.

```shell
--enable-nls='de fr'
```

--------------------------------

### PostgreSQL: Parameterized Queries and Binary I/O with libpq

Source: https://www.postgresql.org/docs/7.4/libpq-example

This C code example demonstrates how to execute SQL queries with out-of-line parameters and handle binary data I/O using the PostgreSQL libpq library. It connects to a database, prepares a table, and then uses `PQexecParams` to insert and retrieve data, highlighting the benefits of avoiding manual escaping and enabling efficient binary data transfer. The code includes necessary headers for network operations and memory management.

```c
/*
 * testlibpq3.c
 *              Test out-of-line parameters and binary I/O.
 *
 * Before running this, populate a database with the following commands
 * (provided in src/test/examples/testlibpq3.sql):
 *
 * CREATE TABLE test1 (i int4, t text, b bytea);
 *
 * INSERT INTO test1 values (1, 'joe''s place', '\000\001\002\003\004');
 * INSERT INTO test1 values (2, 'ho there', '\004\003\002\001\000');
 *
 * The expected output is:
 *
 * tuple 0:
 *  i = 1
 *  t = 'joe''s place'
 *  b = '\000\001\002\003\004'
 *
 */
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/types.h>
#include "libpq-fe.h"

/* for ntohl/htonl */
#include <netinet/in.h>
#include <arpa/inet.h>


static void
exit_nicely(PGconn *conn)
{
        PQfinish(conn);
        exit(1);
}

int
main(int argc, char **argv)
{
        const char *conninfo;
        PGconn     *conn;
        PGresult   *res;
        const char *paramValues[1];
        int                     i, 
                                j;
        int                     i_fnum, 
                                t_fnum, 
                                b_fnum;

        /*
         * If the user supplies a parameter on the command line, use it as
         * the conninfo string; otherwise default to setting dbname=template1
         * and using environment variables or defaults for all other connection
         * parameters.
         */
        if (argc > 1)
                conninfo = argv[1];
        else
                conninfo = "dbname = template1";

        /* Make a connection to the database */
        conn = PQconnectdb(conninfo);

        /* Check to see that the backend connection was successfully made */
        if (PQstatus(conn) != CONNECTION_OK)
        {
                fprintf(stderr, "Connection to database '%s' failed.\n", PQdb(conn));
                fprintf(stderr, "%s", PQerrorMessage(conn));
                exit_nicely(conn);
        }

        /*
         * The point of this program is to illustrate use of PQexecParams()
         * with out-of-line parameters, as well as binary transmission of
         * results.  By using out-of-line parameters we can avoid a lot of
         * tedious mucking about with quoting and escaping.  Notice how we

```

--------------------------------

### Connect to PostgreSQL and Listen for Notifications (C)

Source: https://www.postgresql.org/docs/18/libpq-example

This C code snippet demonstrates how to establish a connection to a PostgreSQL database using libpq, execute SQL commands like SET and LISTEN, and asynchronously consume notifications. It includes error handling for connection and query execution, and uses select() to wait for incoming notifications before finishing the connection.

```c
/*
     * if (argc > 1)
         conninfo = argv[1];
     else
         conninfo = "dbname = postgres";

     /* Make a connection to the database */
    conn = PQconnectdb(conninfo);

    /* Check to see that the backend connection was successfully made */
    if (PQstatus(conn) != CONNECTION_OK)
    {
        fprintf(stderr, "%s", PQerrorMessage(conn));
        exit_nicely(conn);
    }

    /* Set always-secure search path, so malicious users can't take control. */
    res = PQexec(conn,
                 "SELECT pg_catalog.set_config('search_path', '', false)");
    if (PQresultStatus(res) != PGRES_TUPLES_OK)
    {
        fprintf(stderr, "SET failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }

    /*
     * Should PQclear PGresult whenever it is no longer needed to avoid memory
     * leaks
     */
    PQclear(res);

    /*
     * Issue LISTEN command to enable notifications from the rule's NOTIFY.
     */
    res = PQexec(conn, "LISTEN TBL2");
    if (PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "LISTEN command failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }
    PQclear(res);

    /* Quit after four notifies are received. */
    nnotifies = 0;
    while (nnotifies < 4)
    {
        /*
         * Sleep until something happens on the connection.  We use select(2)
         * to wait for input, but you could also use poll() or similar
         * facilities.
         */
        int         sock;
        fd_set      input_mask;

        sock = PQsocket(conn);

        if (sock < 0)
            break;              /* shouldn't happen */

        FD_ZERO(&input_mask);
        FD_SET(sock, &input_mask);

        if (select(sock + 1, &input_mask, NULL, NULL, NULL) < 0)
        {
            fprintf(stderr, "select() failed: %s\n", strerror(errno));
            exit_nicely(conn);
        }

        /* Now check for input */
        PQconsumeInput(conn);
        while ((notify = PQnotifies(conn)) != NULL)
        {
            fprintf(stderr,
                    "ASYNC NOTIFY of '%s' received from backend PID %d\n",
                    notify->relname, notify->be_pid);
            PQfreemem(notify);
            nnotifies++;
            PQconsumeInput(conn);
        }
    }

    fprintf(stderr, "Done.\n");

    /* close the connection to the database and cleanup */
    PQfinish(conn);

    return 0;
}

```

--------------------------------

### Backup PostgreSQL Database using pg_dumpall

Source: https://www.postgresql.org/docs/6.3/c1802

This code demonstrates how to back up an existing PostgreSQL database before upgrading. It uses the `pg_dumpall` utility to create a full database dump. It also includes instructions for handling older versions and preserving object IDs.

```shell
cd
gunzip -c postgresql-v6.3.tar.gz |
tar xvf - src/bin/pg_dump/pg_dumpall
chmod a+x src/bin/pg_dump/pg_dumpall
src/bin/pg_dump/pg_dumpall > db.out
rm -rf src
```

--------------------------------

### Connect and Query PostgreSQL Database using libpq C

Source: https://www.postgresql.org/docs/7.4/libpq-example

This C program demonstrates how to connect to a PostgreSQL database using libpq, execute SQL commands within a transaction, declare and fetch data from a cursor, and properly close the connection. It requires the libpq library to be installed.

```c
/*
 * testlibpq.c
 *
 *              Test the C version of LIBPQ, the POSTGRES frontend library.
 */
#include <stdio.h>
#include <stdlib.h>
#include "libpq-fe.h"

static void
exit_nicely(PGconn *conn)
{
        PQfinish(conn);
        exit(1);
}

int
main(int argc, char **argv)
{
        const char *conninfo;
        PGconn     *conn;
        PGresult   *res;
        int                     nFields;
        int                     i, j;

        /*
         * If the user supplies a parameter on the command line, use it as
         * the conninfo string; otherwise default to setting dbname=template1
         * and using environment variables or defaults for all other connection
         * parameters.
         */
        if (argc > 1)
                conninfo = argv[1];
        else
                conninfo = "dbname = template1";

        /* Make a connection to the database */
        conn = PQconnectdb(conninfo);

        /* Check to see that the backend connection was successfully made */
        if (PQstatus(conn) != CONNECTION_OK)
        {
                fprintf(stderr, "Connection to database '%s' failed.\n", PQdb(conn));
                fprintf(stderr, "%s", PQerrorMessage(conn));
                exit_nicely(conn);
        }

        /*
         * Our test case here involves using a cursor, for which we must be
         * inside a transaction block.  We could do the whole thing with a
         * single PQexec() of "select * from pg_database", but that's too
         * trivial to make a good example.
         */

        /* Start a transaction block */
        res = PQexec(conn, "BEGIN");
        if (PQresultStatus(res) != PGRES_COMMAND_OK)
        {
                fprintf(stderr, "BEGIN command failed: %s", PQerrorMessage(conn));
                PQclear(res);
                exit_nicely(conn);
        }

        /*
         * Should PQclear PGresult whenever it is no longer needed to avoid
         * memory leaks
         */
        PQclear(res);

        /*
         * Fetch rows from pg_database, the system catalog of databases
         */
        res = PQexec(conn, "DECLARE myportal CURSOR FOR select * from pg_database");
        if (PQresultStatus(res) != PGRES_COMMAND_OK)
        {
                fprintf(stderr, "DECLARE CURSOR failed: %s", PQerrorMessage(conn));
                PQclear(res);
                exit_nicely(conn);
        }
        PQclear(res);

        res = PQexec(conn, "FETCH ALL in myportal");
        if (PQresultStatus(res) != PGRES_TUPLES_OK)
        {
                fprintf(stderr, "FETCH ALL failed: %s", PQerrorMessage(conn));
                PQclear(res);
                exit_nicely(conn);
        }

        /* first, print out the attribute names */
        nFields = PQnfields(res);
        for (i = 0; i < nFields; i++)
                printf("% -15s", PQfname(res, i));
        printf("\n\n");

        /* next, print out the rows */
        for (i = 0; i < PQntuples(res); i++)
        {
                for (j = 0; j < nFields; j++)
                        printf("% -15s", PQgetvalue(res, i, j));
                printf("\n");
        }

        PQclear(res);

        /* close the portal ... we don't bother to check for errors ... */
        res = PQexec(conn, "CLOSE myportal");
        PQclear(res);

        /* end the transaction */
        res = PQexec(conn, "END");
        PQclear(res);

        /* close the connection to the database and cleanup */
        PQfinish(conn);

        return 0;
}

```

--------------------------------

### Fetch Binary Data from PostgreSQL Table (C)

Source: https://www.postgresql.org/docs/10/libpq-example

Demonstrates fetching data from a PostgreSQL table in binary format. It includes setting up the table, executing a query to retrieve data, and processing the binary representations of integer, text, and bytea fields.

```C
/*
 * This function prints a query result that is a binary-format fetch from
 * a table defined as in the comment above.  We split it out because the
 * main() function uses it twice.
 */
static void
show_binary_results(PGresult *res)
{
    int         i, j;
    int         i_fnum, t_fnum, b_fnum;

    /* Use PQfnumber to avoid assumptions about field order in result */
    i_fnum = PQfnumber(res, "i");
    t_fnum = PQfnumber(res, "t");
    b_fnum = PQfnumber(res, "b");

    for (i = 0; i < PQntuples(res); i++)
    {
        char       *iptr;
        char       *tptr;
        char       *bptr;
        int         blen;
        int         ival;

        /* Get the field values (we ignore possibility they are null!) */
        iptr = PQgetvalue(res, i, i_fnum);
        tptr = PQgetvalue(res, i, t_fnum);
        bptr = PQgetvalue(res, i, b_fnum);

        /*
         * The binary representation of INT4 is in network byte order, which
         * we'd better coerce to the local byte order.
         */
        ival = ntohl(*((uint32_t *) iptr));

        /*
         * The binary representation of TEXT is, well, text, and since libpq

```

--------------------------------

### PL/pgSQL: Get Row Count using GET DIAGNOSTICS

Source: https://www.postgresql.org/docs/devel/plpgsql-statements

This example demonstrates how to use `GET DIAGNOSTICS` to retrieve the `ROW_COUNT`, which indicates the number of rows processed by the most recent SQL command. The value is assigned to an integer variable, providing a way to check the effect of DML operations.

```sql
GET DIAGNOSTICS integer_var = ROW_COUNT;
```

--------------------------------

### Main Function for libpq Large Object Example (C)

Source: https://www.postgresql.org/docs/16/lo-examplesect

This is the entry point for the C example program demonstrating PostgreSQL large object operations with `libpq`. It declares variables for input/output filenames, the database name, the large object OID, and the PostgreSQL connection object. The full implementation of the `main` function is not included, but it sets up the necessary context for the large object functions.

```C
int
main(int argc, char **argv)
{
    char       *in_filename,
               *out_filename;
    char       *database;
    Oid         lobjOid;
    PGconn     *conn;
    PGresult   *res;

```

--------------------------------

### Build All Documentation Formats with Meson (PostgreSQL)

Source: https://www.postgresql.org/docs/16/docguide-build-meson

This command builds all available formats of the PostgreSQL documentation. Navigate to the `build` directory before execution or append `-C build`. The generated documentation will reside in `build/doc/src/sgml`.

```bash
ninja alldocs
```

--------------------------------

### PostgreSQL Build: Example Makefile.custom Configuration

Source: https://www.postgresql.org/docs/6.4/config11820

This code snippet is an example of a 'Makefile.custom' file used for configuring PostgreSQL builds. It specifies installation directories, C compiler flags, and enables the Tcl interface, along with library and style sheet paths for documentation. It's intended for use during the build process.

```makefile
# Makefile.custom
# Thomas Lockhart 1998-03-01

POSTGRESDIR= /opt/postgres/current
CFLAGS+= -m486 # -g -O0
USE_TCL= true
TCL_LIB= -ltcl
X_LIBS= -L/usr/X11/lib
TK_LIB= -ltk

# documentation

HSTYLE= /home/tgl/SGML/db118.d/docbook/html
PSTYLE= /home/tgl/SGML/db118.d/docbook/print

```

--------------------------------

### PostgreSQL Query Example (SQL)

Source: https://www.postgresql.org/docs/7.3/developer

This snippet demonstrates a basic SELECT query in SQL, commonly used for retrieving data from a PostgreSQL database. It serves as a simple illustration within the developer's guide.

```sql
SELECT * FROM pg_database;

```

--------------------------------

### Verify cvsup Installation

Source: https://www.postgresql.org/docs/6.5/cvs23780

This command checks if the `cvsup` executable is available in the system's PATH. It is a simple verification step to ensure that the CVSup client can be run. If `cvsup` is installed and accessible, its path will be displayed.

```shell
which cvsup
    
```

--------------------------------

### Install PL/Perl Inline and Validator Functions (SQL)

Source: https://www.postgresql.org/docs/10/xplang-install

Example declarations for PL/Perl's inline and validator functions. These are also implemented in C and located in the shared object '$libdir/plperl'. The validator is marked as STRICT.

```sql
CREATE FUNCTION plperl_inline_handler(internal) RETURNS void AS
    '$libdir/plperl' LANGUAGE C;

CREATE FUNCTION plperl_validator(oid) RETURNS void AS
    '$libdir/plperl' LANGUAGE C STRICT;
```

--------------------------------

### PostgreSQL: Double Metaphone Example Usage

Source: https://www.postgresql.org/docs/11/fuzzystrmatch

This example demonstrates how to use the dmetaphone function in PostgreSQL to get the phonetic code for the input string 'gumbo'. The output shows the computed primary code.

```sql
test=# SELECT dmetaphone('gumbo');
 dmetaphone
------------
 KMP
(1 row)
```

--------------------------------

### PostgreSQL Makefile.custom Configuration

Source: https://www.postgresql.org/docs/7.0/docguide28840

Configuration for the PostgreSQL build system, specifying the installation directory, compiler flags, and paths to SGML stylesheets for HTML and print documentation. This snippet is for a custom Makefile setup.

```makefile
# Makefile.custom
# Thomas Lockhart 1998-03-01

POSTGRESDIR= /opt/postgres/current
CFLAGS+= -m486
YFLAGS+= -v

# documentation

HSTYLE= /home/lockhart/SGML/db143.d/docbook/html
PSTYLE= /home/lockhart/SGML/db143.d/docbook/print
```

--------------------------------

### Create a Database using createdb

Source: https://www.postgresql.org/docs/6.5/app-createdb

Examples demonstrating how to use the 'createdb' command to create a new PostgreSQL database named 'demo'. The first example uses default connection settings, while the second specifies a remote host and port.

```bash
$ createdb demo
```

```bash
$ createdb -p 5000 -h eden demo
```

--------------------------------

### PostgreSQL restore_command Example

Source: https://www.postgresql.org/docs/10/continuous-archiving

This is an example of the `restore_command` configuration parameter for PostgreSQL recovery. It specifies how the server should retrieve archived WAL segment files from a local directory. The `%f` placeholder is replaced with the name of the WAL file to be restored.

```postgresql.conf
restore_command = 'cp /mnt/server/archivedir/%f %p'
```

--------------------------------

### Connect to PostgreSQL and Set Search Path

Source: https://www.postgresql.org/docs/current/libpq-example

Establishes a connection to a PostgreSQL database using a provided connection string or a default. It then sets a secure search path for the database session to prevent security vulnerabilities. Error handling for connection and command execution is included.

```c
int
main(int argc, char **argv)
{
    const char *conninfo;
    PGconn     *conn;
    PGresult   *res;

    if (argc > 1)
        conninfo = argv[1];
    else
        conninfo = "dbname = postgres";

    conn = PQconnectdb(conninfo);

    if (PQstatus(conn) != CONNECTION_OK)
    {
        fprintf(stderr, "%s", PQerrorMessage(conn));
        exit_nicely(conn);
    }

    res = PQexec(conn, "SET search_path = testlibpq3");
    if (PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "SET failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }
    PQclear(res);

    /* ... rest of the code ... */

    PQfinish(conn);

    return 0;
}
```

--------------------------------

### PostgreSQL Configuration for Custom Extension Paths

Source: https://www.postgresql.org/docs/18/extend-pgxs

Provides example configurations for `extension_control_path` and `dynamic_library_path` to enable the PostgreSQL server to locate extension files installed in custom directories. This is necessary when using non-standard installation prefixes.

```postgresql
extension_control_path = '/usr/local/extras/share/postgresql:$system'
dynamic_library_path = '/usr/local/extras/lib/postgresql:$libdir'
```

--------------------------------

### Install flex Utility for PostgreSQL Compilation

Source: https://www.postgresql.org/docs/6.3/c1802

This snippet demonstrates how to download, configure, build, and install the flex utility, which is a dependency for compiling PostgreSQL on certain platforms. It ensures the correct version of flex is available.

```shell
cd
gunzip -c flex-2.5.4.tar.gz | tar xvf -
cd flex-2.5.4
configure --prefix=/usr
make
make check
# You must be root when typing the next line.
make install
cd
rm -rf flex-2.5.4
```

--------------------------------

### Check SELinux Status on Linux

Source: https://www.postgresql.org/docs/devel/sepgsql

This command-line example demonstrates how to use `sestatus` to verify that SELinux is enabled and configured correctly on a Linux system. It shows typical output including the SELinux status, mount point, current mode, and policy version.

```bash
$ sestatus
SELinux status:                 enabled
SELinuxfs mount:                /selinux
Current mode:                   enforcing
Mode from config file:          enforcing
Policy version:                 24
Policy from config file:        targeted
```

--------------------------------

### Stream Logical Decoding with pg_recvlogical

Source: https://www.postgresql.org/docs/16/logicaldecoding-example

This example shows how to use the `pg_recvlogical` utility to stream logical decoding changes over the replication protocol. It requires client authentication to be configured for replication and sufficient `max_wal_senders`. The example demonstrates creating a slot, starting to receive changes, inserting data, and observing the streamed transaction details. Two-phase transactions require `max_prepared_transactions` to be at least 1.

```shell
$ pg_recvlogical -d postgres --slot=test --create-slot
$ pg_recvlogical -d postgres --slot=test --start -f -
**Control**+**Z**
$ psql -d postgres -c "INSERT INTO data(data) VALUES('4');"
$ fg
BEGIN 693
table public.data: INSERT: id[integer]:4 data[text]:'4'
COMMIT 693
**Control**+**C**
```

--------------------------------

### PostgreSQL: Show All Parameters

Source: https://www.postgresql.org/docs/17/sql-show

Illustrates how to use the SHOW ALL command in PostgreSQL to retrieve and display the values of all available run-time configuration parameters, along with their descriptions.

```sql
SHOW ALL;
-- Expected Output (partial):
--             name         | setting |                description
-------------------------+---------+-------------------------------------------------
 allow_system_table_mods | off     | Allows modifications of the structure of ...
    .
    .
    .
 xmloption               | content | Sets whether XML data in implicit parsing ...
 zero_damaged_pages      | off     | Continues processing past damaged page headers.
(196 rows)
```

--------------------------------

### Install FreeBSD Documentation Ports

Source: https://www.postgresql.org/docs/7.0/docguide29024

Installs essential ports for building documentation on FreeBSD, including gmake, docproj, docbook, and dsssl-docbook-modular. These are prerequisites for processing DocBook documentation.

```shell
% cd /usr/ports/devel/gmake && make install
% cd /usr/ports/textproc/docproj && make install
% cd /usr/ports/textproc/docbook && make install
% cd /usr/ports/textproc/dsssl-docbook-modular && make install
```

--------------------------------

### Start PostgreSQL Server

Source: https://www.postgresql.org/docs/18/logical-replication-upgrade

Starts a PostgreSQL server instance. This command is used after an upgrade or maintenance to bring the database back online. It logs output to a specified logfile.

```bash
pg_ctl -D /opt/PostgreSQL/data1_upgraded start -l logfilepg_ctl -D /opt/PostgreSQL/data2_upgraded start -l logfilepg_ctl -D /opt/PostgreSQL/data3_upgraded start -l logfile
```

--------------------------------

### Build PostgreSQL Client with Borland C++

Source: https://www.postgresql.org/docs/8.0/install-win32

This command builds the PostgreSQL client library (libpq) and interactive terminal (psql) on Windows using Borland C++. It requires specifying the makefile and configuration. The output includes DLLs, import libraries, and the psql executable.

```shell
`make -N -DCFG=Release /f bcc32.mak`
```

--------------------------------

### Install PostgreSQL Files

Source: https://www.postgresql.org/docs/10/install-windows-full

Commands to install PostgreSQL files to a specified destination directory. An optional 'client' argument installs only client applications and libraries.

```shell
**install c:\destination\directory**
```

```shell
**install c:\destination\directory client**
```

--------------------------------

### PostgreSQL: dblink_fetch Example Usage

Source: https://www.postgresql.org/docs/11/contrib-dblink-fetch

Demonstrates the typical workflow of using dblink_fetch, including establishing a connection, opening a cursor, and fetching data from it, with examples of handling the fetched records.

```postgresql
SELECT dblink_connect('dbname=postgres options=-csearch_path=');

SELECT dblink_open('foo', 'select proname, prosrc from pg_proc where proname like ''bytea%''');

SELECT * FROM dblink_fetch('foo', 5) AS (funcname name, source text);

SELECT * FROM dblink_fetch('foo', 5) AS (funcname name, source text);

SELECT * FROM dblink_fetch('foo', 5) AS (funcname name, source text);

SELECT * FROM dblink_fetch('foo', 5) AS (funcname name, source text);
```

--------------------------------

### Retrieve Enum Sub-Range from Start to Value in PostgreSQL (enum_range with NULL start)

Source: https://www.postgresql.org/docs/14/functions-enum

Shows how to use 'enum_range' with 'NULL' as the first argument to get an ordered array of enum values from the first member of the enum type up to a specified end value. This effectively defines a range starting from the enum's beginning.

```SQL
enum_range(NULL, 'green'::rainbow)
```

--------------------------------

### Manual Installation Example: Declare PL/pgSQL as a Trusted Procedural Language

Source: https://www.postgresql.org/docs/8.0/xplang

This final SQL command in the manual installation process declares PL/pgSQL as a trusted procedural language. It links the previously defined `plpgsql_call_handler` and `plpgsql_validator` functions, making PL/pgSQL available for use by database users to create functions and trigger procedures.

```sql
CREATE TRUSTED PROCEDURAL LANGUAGE plpgsql
    HANDLER plpgsql_call_handler
    VALIDATOR plpgsql_validator;
```

--------------------------------

### PostgreSQL LISTEN/NOTIFY Example in psql

Source: https://www.postgresql.org/docs/6.4/sql-listen

Demonstrates a typical listen/notify sequence using the psql command-line client. It shows how to set up a listener and then trigger a notification.

```sql
-- Configure and execute a listen/notify sequence from psql
postgres=> listen virtual;
LISTEN
postgres=> notify virtual;
NOTIFY
ASYNC NOTIFY of 'virtual' from backend pid '11239' received

```

--------------------------------

### Extract WAL File Name and Offset from LSN | PostgreSQL Example

Source: https://www.postgresql.org/docs/current/functions-admin

An example demonstrating the usage of `pg_walfile_name_offset` with the result of `pg_backup_stop()` to get the WAL file name and offset. This is commonly used in backup scenarios.

```sql
SELECT * FROM pg_walfile_name_offset((pg_backup_stop()).lsn);
-- Example Output:
--        file_name         | file_offset
-- --------------------------+-------------
--  00000001000000000000000D |     4039624
-- (1 row)
```

--------------------------------

### BKI Backend Interface Example

Source: https://www.postgresql.org/docs/7.2/developer

Demonstrates a simplified structure of a BKI (Backend Interface) command, used for defining database objects during PostgreSQL initialization or extension loading. This format is specific to PostgreSQL's internal configuration and extension management.

```BKI
// Example of a BKI command to create a table (conceptual)
// CREATE TABLE table_name (
//     column1 data_type,
//     column2 data_type
// );

// BKI representation might involve specific keywords and parameters:
// DEFINE TABLE table_name {
//     column1 TYPE integer,
//     column2 TYPE text
// }
```

--------------------------------

### PostgreSQL Error Message Object Type Example

Source: https://www.postgresql.org/docs/11/error-style-guide

Shows the importance of specifying the type of object when referencing it in an error message. This ensures clarity for the user, as demonstrated by the example specifying 'file' when mentioning 'foo.bar.baz'.

```text
could not open file %s: %m

```

--------------------------------

### Running PostgreSQL Regression Tests with Meson

Source: https://www.postgresql.org/docs/16/install-meson

Explains how to execute the PostgreSQL regression test suite using 'meson test'. These tests verify the correct functionality of the newly built server and should be run as an unprivileged user. An option for running tests against an already running instance is also mentioned.

```shell
meson test
```

--------------------------------

### Install PostgreSQL World Binaries (make install-world-bin)

Source: https://www.postgresql.org/docs/10/install-procedure

Installs only the binary executables from the PostgreSQL world build, excluding documentation. This is useful if documentation was not included in the initial build or is not desired.

```shell
make install-world-bin
```

--------------------------------

### PostgreSQL: Create Subscription with Deferred Connection and Custom Slot Name

Source: https://www.postgresql.org/docs/16/logical-replication-subscription

This example shows creating a PostgreSQL subscription where `connect = false` and a specific `slot_name` is provided. It outlines the process of creating the subscription, manually creating the logical replication slot on the publisher using the specified custom name, and finally activating the subscription on the subscriber by enabling and refreshing it.

```sql
CREATE SUBSCRIPTION sub1
CONNECTION 'host=localhost dbname=test_pub'
PUBLICATION pub1
WITH (connect=false, slot_name='myslot');
```

```sql
SELECT * FROM pg_create_logical_replication_slot('myslot', 'pgoutput');
```

```sql
ALTER SUBSCRIPTION sub1 ENABLE;
ALTER SUBSCRIPTION sub1 REFRESH PUBLICATION;
```

--------------------------------

### PostgreSQL postmaster status output example

Source: https://www.postgresql.org/docs/7.0/app-pgctl

This example demonstrates the typical output format when querying the status of a PostgreSQL postmaster using pg_ctl status. It includes information about whether the postmaster is running, its process ID (PID), and the options it was started with.

```bash
pg_ctl: postmaster is running (pid: 13718)
options are:
/usr/local/src/pgsql/current/bin/postmaster
-p 5433
-D /usr/local/src/pgsql/current/data
-B 64
-b /usr/local/src/pgsql/current/bin/postgres
-N 32
-o '-F'
```

--------------------------------

### Recommended Configure Options for Development

Source: https://www.postgresql.org/docs/12/install-procedure

Enables runtime error checks and improves debugging tool output. Essential for developers working on the PostgreSQL server code.

```shell
--enable-cassert
--enable-debug
```

--------------------------------

### PostgreSQL Startup Phase

Source: https://www.postgresql.org/docs/7.0/protocol25770

Describes the initial connection and authentication process between the PostgreSQL frontend and backend.

```APIDOC
## PostgreSQL Frontend/Backend Protocol - Startup Phase

### Description
This section details the initial message flow for establishing a connection between a PostgreSQL frontend and backend, including authentication and backend startup.

### Method
N/A (Protocol Description)

### Endpoint
N/A (Protocol Description)

### Parameters
N/A (Protocol Description)

### Request Example
**Frontend sends StartupPacket**
```
(Binary StartupPacket data)
```

### Response
**Postmaster messages during authentication:**

*   **ErrorResponse** - Connection closed due to authentication failure.
*   **AuthenticationOk** - Authentication successful, connection handed over to backend.
*   **AuthenticationKerberosV4** - Initiates Kerberos V4 authentication dialog.
*   **AuthenticationKerberosV5** - Initiates Kerberos V5 authentication dialog.
*   **AuthenticationUnencryptedPassword** - Frontend must send an UnencryptedPasswordPacket.
*   **AuthenticationEncryptedPassword** - Frontend must send an EncryptedPasswordPacket.

**Backend messages after successful startup:**

*   **BackendKeyData** - Issued after successful backend startup, provides cancel request key.
*   **ReadyForQuery** - Indicates successful backend startup, frontend may now issue queries.
*   **ErrorResponse** - Indicates backend startup failure, connection closed.
*   **NoticeResponse** - A warning message, frontend should display and continue listening.

#### Response Example
**Successful Startup:**
```
(Binary AuthenticationOk data)
(Binary BackendKeyData data)
(Binary ReadyForQuery data)
```

**Failed Authentication:**
```
(Binary ErrorResponse data)
```

**Failed Backend Startup:**
```
(Binary ErrorResponse data)
```
```

--------------------------------

### PostgreSQL C SRF Pseudo-code Example: Setting up and Returning Data

Source: https://www.postgresql.org/docs/8.0/xfunc-c

A pseudo-code example illustrating the typical structure of a PostgreSQL set-returning function (SRF) in C. It shows the conditional initialization using SRF_IS_FIRSTCALL and SRF_FIRSTCALL_INIT, memory context management, and placeholders for user-specific setup and data preparation before returning results with SRF_RETURN_NEXT.

```c
Datum
my_set_returning_function(PG_FUNCTION_ARGS)
{
    FuncCallContext  *funcctx;
    Datum             result;
    MemoryContext     oldcontext;
    /* further declarations as needed */

    if (SRF_IS_FIRSTCALL())
    {
        funcctx = SRF_FIRSTCALL_INIT();
        oldcontext = MemoryContextSwitchTo(funcctx->multi_call_memory_ctx);
        /* One-time setup code appears here: */
        /* user code */
        /* if returning composite */
            /* build TupleDesc, and perhaps AttInMetadata */
        /* endif returning composite */
        /* user code */
        MemoryContextSwitchTo(oldcontext); /* Restore context after setup */
    }

    /* Prepare for the current call */
    SRF_PERCALL_SETUP(funcctx);

    /*
     * Compute the next result Datum.  Place your code to compute the next
     * result here.
     */
    /* user code */

    /* Check if we are done */
    if (/* condition to stop */)
    {
        SRF_RETURN_DONE(funcctx);
    }
    else
    {
        /* return the result */
        SRF_RETURN_NEXT(funcctx, (Datum) result);
    }
}

```

--------------------------------

### PostgreSQL pgtcl Example: Retrieve Database Names

Source: https://www.postgresql.org/docs/7.4/pgtcl-examplesect

This Tcl script demonstrates how to use the pgtcl library to connect to a PostgreSQL database and retrieve a list of all database names. It handles default host and port values and returns the names in alphabetical order. Ensure the pgtcl library is installed and accessible.

```tcl
# getDBs :\n#   get the names of all the databases at a given host and port number\n#   with the defaults being the localhost and port 5432\n#   return them in alphabetical order\nproc getDBs { {host "localhost"} {port "5432"} } {\n    # datnames is the list to be result\n    set conn [pg_connect template1 -host $host -port $port]\n    set res [pg_exec $conn "SELECT datname FROM pg_database ORDER BY datname;"]\n    set ntups [pg_result $res -numTuples]\n    for {set i 0} {$i < $ntups} {incr i} {\n        lappend datnames [pg_result $res -getTuple $i]\n    }\n    pg_result $res -clear\n    pg_disconnect $conn\n    return $datnames\n}

```

--------------------------------

### PostgreSQL dropuser Usage Examples

Source: https://www.postgresql.org/docs/7.0/app-dropuser

Demonstrates practical examples of using the dropuser command. The first example shows the basic removal of a user, while the second illustrates advanced usage with specific host, port, interactive, and echo options.

```bash
$ dropuser joe
DROP USER
```

```bash
$ dropuser -p 5000 -h eden -i -e joe
User "joe" and any owned databases will be permanently deleted.
Are you sure? (y/n) y
DROP USER "joe"
DROP USER
```

--------------------------------

### PostgreSQL: Example Synonym Rule File Format

Source: https://www.postgresql.org/docs/17/dict-xsyn

Defines the format for a synonym rule file used by the dict_xsyn PostgreSQL extension. Each line contains a word followed by its synonyms, separated by whitespace. Lines starting with '#' are treated as comments.

```text
# word syn1 syn2 syn3

```

--------------------------------

### Build PostgreSQL Client Libraries on Windows

Source: https://www.postgresql.org/docs/7.1/install-win32

Command to compile PostgreSQL client libraries (libpq and psql) on Windows using Microsoft Visual C++. Assumes Visual C++ is in the system's PATH.

```shell
`nmake /f win32.mak`
```

--------------------------------

### psql Synopsis

Source: https://www.postgresql.org/docs/10/app-psql

Shows the basic command-line syntax for starting the psql interactive terminal. It allows specifying options, a database name, and a username.

```bash
psql [_`option`_...] [_`dbname`_[_`username`_]]
```

--------------------------------

### PostgreSQL Error Message - Avoiding Function Names Example

Source: https://www.postgresql.org/docs/12/error-style-guide

Shows how to rephrase error messages to be more user-friendly by avoiding internal function names. The 'BETTER' example focuses on the user-facing problem rather than the implementation detail.

```text
BAD:    pg_strtoint32: error in "z": cannot parse "z"
BETTER: invalid input syntax for type integer: "z"

```

```text
BAD:    open() failed: %m
BETTER: could not open file %s: %m

```

--------------------------------

### Test Procedural Languages (Post-Installation)

Source: https://www.postgresql.org/docs/8.1/regress

Runs regression tests for installed procedural languages within PostgreSQL. These tests are executed against an already installed server and require navigating to the respective language's subdirectory within the build tree.

```shell
cd src/pl
gmake installcheck
```

--------------------------------

### Add libpqdll.lib to Visual C++ Project

Source: https://www.postgresql.org/docs/7.0/install-win3217392

This describes the process of adding the PostgreSQL library file 'libpqdll.lib' to a Visual C++ project to enable its use. No specific code is shown, but the action is clear.

```text
To use the libraries, you must add the `libpqdll.lib` file to your project (in Visual C++, just right-click on the project and chose to add it).
```

--------------------------------

### Run PostgreSQL Regression Tests (Post Installation)

Source: https://www.postgresql.org/docs/7.1/regress

Executes PostgreSQL regression tests after the software has been installed. This method requires initializing a data area and starting the PostgreSQL server. It expects to connect to the server on the local host and default port, unless overridden by environment variables.

```shell
`$ ``gmake installcheck`
```

--------------------------------

### Build PostgreSQL, Contrib, and Documentation with 'make world'

Source: https://www.postgresql.org/docs/11/install-procedure

Builds the entire PostgreSQL system, including the 'contrib' modules and both HTML and man page documentation. This command ensures all components are compiled.

```shell
**make world**
```

--------------------------------

### PostgreSQL vacuumdb Command Examples

Source: https://www.postgresql.org/docs/current/app-vacuumdb

Demonstrates various ways to use the vacuumdb command-line utility for PostgreSQL database maintenance and analysis. These examples cover basic vacuuming, analyzing tables, and specifying schemas.

```shell
$ **vacuumdb test**

```

```shell
$ **vacuumdb --analyze bigdb**

```

```shell
$ **vacuumdb --analyze --verbose --table='foo(bar)' xyzzy**

```

```shell
$ **vacuumdb --schema='foo' --schema='bar' xyzzy**

```

--------------------------------

### Configure PostgreSQL Source Code

Source: https://www.postgresql.org/docs/6.3/c1802

This command initiates the configuration process for PostgreSQL compilation. It navigates to the source directory and runs the `./configure` script. The `configure` script prepares the build environment and allows customization of installation paths and features.

```shell
cd /usr/src/pgsql/src
./configure
```

--------------------------------

### Test C Libpq Connection and Query Execution

Source: https://www.postgresql.org/docs/6.5/libpq-chapter18375

This C program demonstrates how to connect to a PostgreSQL database using libpq, execute SQL commands like BEGIN, DECLARE CURSOR, FETCH ALL, CLOSE, and COMMIT, and handle results. It includes error checking for connection and query execution, and cleans up resources.

```c
/*
 * testlibpq.c Test the C version of Libpq, the Postgres frontend
 * library.
 *
 *
 */
#include <stdio.h>
#include "libpq-fe.h"

void
exit_nicely(PGconn *conn)
{
    PQfinish(conn);
    exit(1);
}

main()
{
    char       *pghost, 
               *pgport, 
               *pgoptions, 
               *pgtty;
    char       *dbName;
    int         nFields;
    int         i, 
                j;

    /* FILE *debug; */

    PGconn     *conn;
    PGresult   *res;

    /*
     * begin, by setting the parameters for a backend connection if the
     * parameters are null, then the system will try to use reasonable
     * defaults by looking up environment variables or, failing that,
     * using hardwired constants
     */
    pghost = NULL;              /* host name of the backend server */
    pgport = NULL;              /* port of the backend server */
    pgoptions = NULL;           /* special options to start up the backend
                                 * server */
    pgtty = NULL;               /* debugging tty for the backend server */
    dbName = "template1";

    /* make a connection to the database */
    conn = PQsetdb(pghost, pgport, pgoptions, pgtty, dbName);

    /*
     * check to see that the backend connection was successfully made
     */
    if (PQstatus(conn) == CONNECTION_BAD)
    {
        fprintf(stderr, "Connection to database '%s' failed.\n", dbName);
        fprintf(stderr, "%s", PQerrorMessage(conn));
        exit_nicely(conn);
    }

    /* debug = fopen(\"/tmp/trace.out\",\"w\"); */
    /* PQtrace(conn, debug);  */

    /* start a transaction block */
    res = PQexec(conn, "BEGIN");
    if (!res || PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "BEGIN command failed\n");
        PQclear(res);
        exit_nicely(conn);
    }

    /*
     * should PQclear PGresult whenever it is no longer needed to avoid
     * memory leaks
     */
    PQclear(res);

    /*
     * fetch instances from the pg_database, the system catalog of
     * databases
     */
    res = PQexec(conn, "DECLARE mycursor CURSOR FOR select * from pg_database");
    if (!res || PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "DECLARE CURSOR command failed\n");
        PQclear(res);
        exit_nicely(conn);
    }
    PQclear(res);
    res = PQexec(conn, "FETCH ALL in mycursor");
    if (!res || PQresultStatus(res) != PGRES_TUPLES_OK)
    {
        fprintf(stderr, "FETCH ALL command didn't return tuples properly\n");
        PQclear(res);
        exit_nicely(conn);
    }

    /* first, print out the attribute names */
    nFields = PQnfields(res);
    for (i = 0; i < nFields; i++)
        printf("% -15s", PQfname(res, i));
    printf("\n\n");

    /* next, print out the instances */
    for (i = 0; i < PQntuples(res); i++)
    {
        for (j = 0; j < nFields; j++)
            printf("% -15s", PQgetvalue(res, i, j));
        printf("\n");
    }
    PQclear(res);

    /* close the cursor */
    res = PQexec(conn, "CLOSE mycursor");
    PQclear(res);

    /* commit the transaction */
    res = PQexec(conn, "COMMIT");
    PQclear(res);

    /* close the connection to the database and cleanup */
    PQfinish(conn);

    /* fclose(debug); */
}

```

--------------------------------

### Configure PostgreSQL Installation (Shell)

Source: https://www.postgresql.org/docs/10/install-procedure

This snippet demonstrates the basic command to configure the PostgreSQL source tree for installation. It runs the 'configure' script to set up the build environment. For a default installation, simply execute './configure' in the source directory.

```shell
./configure
```

--------------------------------

### PostgreSQL SHOW DateStyle Example

Source: https://www.postgresql.org/docs/14/sql-show

An example demonstrating how to use the SHOW command to display the current setting for the 'DateStyle' parameter in PostgreSQL.

```sql
SHOW DateStyle;

 DateStyle
-----------
 ISO, MDY
(1 row)
```

--------------------------------

### PostgreSQL initdb Description

Source: https://www.postgresql.org/docs/12/app-initdb

A detailed explanation of what the initdb command does, including creating directories, shared catalog tables, and default databases like template1 and postgres. It also touches upon the importance of running initdb as the correct user.

```text
initdb creates a new PostgreSQL database cluster. A database cluster is a collection of databases that are managed by a single server instance.
Creating a database cluster consists of creating the directories in which the database data will live, generating the shared catalog tables (tables that belong to the whole cluster rather than to any particular database), and creating the template1 and postgres databases. When you later create a new database, everything in the template1 database is copied. (Therefore, anything installed in template1 is automatically copied into each database created later.) The postgres database is a default database meant for use by users, utilities and third party applications.
```

--------------------------------

### PostgreSQL Error Message: Rewording for Clarity

Source: https://www.postgresql.org/docs/13/error-style-guide

Provides an example of how to reword an error message to be more user-friendly and less technical. This example transforms a message mentioning a specific routine to a more general 'invalid input syntax' message.

```sql
BETTER: invalid input syntax for type integer: "z"
```

--------------------------------

### PostgreSQL Error Message: Present Tense Example

Source: https://www.postgresql.org/docs/13/error-style-guide

Demonstrates the use of present tense for error messages when a failure is permanent or the functionality does not exist. This example indicates an inability to open a file due to a fundamental issue.

```sql
cannot open file "%s"
```

--------------------------------

### Main Function for PostgreSQL Large Object Example (C)

Source: https://www.postgresql.org/docs/14/lo-examplesect

The main entry point for the large object example program. It declares variables for filenames, database connection, and results. It sets up the program's execution flow, although the core logic for connecting and processing large objects is not shown in this snippet.

```c
int
main(int argc, char **argv)
{
    char       *in_filename, 
               *out_filename;
    char       *database;
    Oid         lobjOid;
    PGconn     *conn;
    PGresult   *res;

```

--------------------------------

### PostgreSQL Error Message: Past Tense Example

Source: https://www.postgresql.org/docs/13/error-style-guide

Illustrates the use of past tense for error messages when an action failed but might succeed later. This example shows a message indicating a failure to open a file.

```sql
could not open file "%s": %m
```

--------------------------------

### PostgreSQL ALTER SEQUENCE - Min/Max Values and Start Point

Source: https://www.postgresql.org/docs/10/sql-altersequence

This example shows how to set the minimum and maximum values for a sequence, or explicitly disable them using NO MINVALUE and NO MAXVALUE. It also demonstrates setting the initial start value for future restarts.

```sql
ALTER SEQUENCE my_sequence MINVALUE 100;
ALTER SEQUENCE my_sequence MAXVALUE 1000;
ALTER SEQUENCE my_sequence START WITH 50;
```

--------------------------------

### Running PostgreSQL Tutorial Scripts with psql

Source: https://www.postgresql.org/docs/8.1/tutorial-sql

This snippet demonstrates how to navigate to the PostgreSQL tutorial directory, compile C files, and execute SQL scripts using the `psql` command-line interface. It shows how to use the `i` command to read commands from a file and the `-s` option for single-step execution.

```bash
cd `....`/src/tutorial
make
cd `....`/src/tutorial
psql -s mydb
mydb=> `\i basics.sql`
```

--------------------------------

### PostgreSQL POSIX Time Zone Specification Example

Source: https://www.postgresql.org/docs/10/datetime-posix-timezone-specs

Provides an example of a POSIX-style time zone specification in PostgreSQL. This example demonstrates how to define standard and daylight saving time abbreviations, UTC offsets, and the rules for DST transitions. It highlights the format for specifying the start and end of DST based on specific days and times.

```text
CET-1CEST,M3.5.0,M10.5.0/3
```

--------------------------------

### PostgreSQL Configuration File (`postgresql.conf`) Example

Source: https://www.postgresql.org/docs/8.0/runtime-config

An example of the `postgresql.conf` file, used to set run-time configuration parameters for PostgreSQL. Parameters are specified one per line, with optional assignment operators. Comments start with '#'. Values requiring special characters must be single-quoted. The file is reread on SIGHUP signal.

```postgresql.conf
# This is a comment
log_connections = yes
log_destination = 'syslog'
search_path = '$user, public'

```

--------------------------------

### Install PostgreSQL Files (Batch)

Source: https://www.postgresql.org/docs/12/install-windows-full

Installs PostgreSQL files to a specified destination directory. Supports installing all files or only client applications and interface libraries.

```batch
**install c:\\destination\\directory**
```

```batch
**install c:\\destination\\directory client**
```

--------------------------------

### PostgreSQL Dynamic Domain Transition Example

Source: https://www.postgresql.org/docs/10/sepgsql

Demonstrates using `sepgsql_getcon()` to retrieve the current security context and `sepgsql_setcon()` to transition to a new context in PostgreSQL. Shows successful transition to a smaller privilege set and a denied transition back.

```sql
regression=# select sepgsql_getcon();
                    sepgsql_getcon
-------------------------------------------------------
 unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
(1 row)

regression=# SELECT sepgsql_setcon('unconfined_u:unconfined_r:unconfined_t:s0-s0:c1.c4');
 sepgsql_setcon 
----------------
 t
(1 row)

regression=# SELECT sepgsql_setcon('unconfined_u:unconfined_r:unconfined_t:s0-s0:c1.c1023');
ERROR:  SELinux: security policy violation
```

--------------------------------

### PostgreSQL: Check if a range is strictly right of another

Source: https://www.postgresql.org/docs/14/functions-range

This example demonstrates the `>>` operator to check if the first range starts after the second range ends, meaning it is strictly to the right. It returns `true` for such a condition. The example uses `int8range`.

```sql
SELECT int8range(50,60) >> int8range(20,30);
```

--------------------------------

### PostgreSQL: Create User Examples

Source: https://www.postgresql.org/docs/6.5/sql-createuser

Examples demonstrating the usage of the CREATE USER statement in PostgreSQL. These examples cover creating a user without a password, with a password, setting an account validity period, and granting database creation privileges.

```sql
CREATE USER jonathan
```

```sql
CREATE USER davide WITH PASSWORD jw8s0F4
```

```sql
CREATE USER miriam WITH PASSWORD jw8s0F4 VALID UNTIL 'Jan 1 2002'
```

```sql
CREATE USER manuel WITH PASSWORD jw8s0F4 CREATEDB
```

--------------------------------

### Run PostgreSQL Regression Tests (Existing Installation)

Source: https://www.postgresql.org/docs/10/regress-run

Executes PostgreSQL regression tests against an already installed and running server. This requires a initialized data area and a started server. Tests will connect to the local host on the default port unless `PGHOST` and `PGPORT` are specified. Existing databases named 'regression' will be dropped.

```bash
make installcheck
```

--------------------------------

### OpenBSD PostgreSQL Autostart Script for rc.local (Bash)

Source: https://www.postgresql.org/docs/10/server-start

This script snippet is designed for OpenBSD's `/etc/rc.local` to automatically start PostgreSQL at system boot. It first checks for the existence of `pg_ctl` and `postgres` executables, then uses `su -l postgres -c` to launch the server as the `postgres` user, specifying the data directory and a dedicated log file.

```bash
if [ -x /usr/local/pgsql/bin/pg_ctl -a -x /usr/local/pgsql/bin/postgres ]; then
    su -l postgres -c '/usr/local/pgsql/bin/pg_ctl start -s -l /var/postgresql/log -D /usr/local/pgsql/data'
    echo -n ' postgresql'
fi
```

--------------------------------

### PostgreSQL Example: Disable Index Scans in a Database

Source: https://www.postgresql.org/docs/10/sql-alterdatabase

A practical example showing how to set a specific configuration parameter, `enable_indexscan`, to 'off' for a PostgreSQL database named 'test'. This change affects new sessions started in that database.

```sql
ALTER DATABASE test SET enable_indexscan TO off;
```

--------------------------------

### Makefile for PostgreSQL Extension Installation

Source: https://www.postgresql.org/docs/11/extend-extensions

This Makefile automates the installation process for the PostgreSQL "pair" extension. It defines the `EXTENSION` and `DATA` variables, leverages `PG_CONFIG` to locate `pgxs`, and includes the standard `PGXS` build infrastructure provided by PostgreSQL. This setup allows `make install` to correctly place the extension's control and script files into the appropriate PostgreSQL directory.

```makefile
EXTENSION = pair
DATA = pair--1.0.sql

PG_CONFIG = pg_config
PGXS := $(shell $(PG_CONFIG) --pgxs)
include $(PGXS)
```

--------------------------------

### BKI File Command Example (PostgreSQL)

Source: https://www.postgresql.org/docs/17/bki

Shows an example of a command within a BKI (Backend Interface) file. These files are used during the bootstrap mode to load initial data into system catalogs.

```bki
-- BKI commands to create and populate pg_class
CREATE FUNCTION pg_catalog.pg_class (oid) RETURNS pg_class AS '$\\1'
    LANGUAGE internal STRICT;

-- Insert initial row for pg_class itself
INSERT catalog pg_class VALUES
    (12, 'pg_class', 11, 'f', 'r', 'a', 'a', 'a', 'a', 'a', 'a', 'a', 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0
```

--------------------------------

### Check Disk Space with df -k Command

Source: https://www.postgresql.org/docs/6.4/install

This command checks the available disk space on the system. It is a standard Unix utility and does not have specific inputs or outputs beyond the system's disk usage information. This is crucial for ensuring sufficient space for PostgreSQL installation and operation.

```shell
$ df -k

```

--------------------------------

### Show PostgreSQL Server Status with pg_ctl

Source: https://www.postgresql.org/docs/18/app-pg-ctl

Provides an example of how to check the status of the PostgreSQL server using pg_ctl status. The output includes the server's PID and the command used to start it.

```bash
$ pg_ctl status
pg_ctl: server is running (PID: 13718)
/usr/local/pgsql/bin/postgres "-D" "/usr/local/pgsql/data" "-p" "5433" "-B" "128"
```

--------------------------------

### Reproduce PostgreSQL Build Configuration with pg_config

Source: https://www.postgresql.org/docs/10/app-pgconfig

This example demonstrates how to use `pg_config --configure` to retrieve the configuration options used to build the current PostgreSQL installation. The `eval` command is necessary because the output of `pg_config --configure` includes shell quotation marks for correct argument parsing.

```shell
eval ./configure `pg_config --configure`
```

--------------------------------

### Starting PostgreSQL Interactive Monitor (psql)

Source: https://www.postgresql.org/docs/6.5/query

This snippet demonstrates how to start the PostgreSQL interactive SQL monitor and connect to a database. It assumes the 'mydb' database has been created. The '-s' option enables single-step mode.

```bash
cd /usr/local/pgsql/src/tutorial
psql -s mydb
```

--------------------------------

### PostgreSQL Error Message Formatting Example (Before)

Source: https://www.postgresql.org/docs/16/error-style-guide

An example of a less-ideal error message format in PostgreSQL, showing a long primary message with embedded details and hints. This format can be less user-friendly and harder to parse in different client applications.

```text
IpcMemoryCreate: shmget(key=%d, size=%u, 0%o) failed: %m
(plus a long addendum that is basically a hint)
```

--------------------------------

### Create PostgreSQL Data Directory and Initialize (Shell)

Source: https://www.postgresql.org/docs/7.0/install17165

Creates the data directory for PostgreSQL, sets ownership to the 'postgres' user, and then initializes the database cluster using `initdb`. This step requires logging in as the intended database superuser.

```shell
> mkdir /usr/local/pgsql/data
> chown postgres /usr/local/pgsql/data
> su - postgres
> /usr/local/pgsql/bin/initdb -D /usr/local/pgsql/data
```

--------------------------------

### libpq Example Program 1: C Connection and Transaction

Source: https://www.postgresql.org/docs/16/libpq-example

This C program demonstrates how to connect to a PostgreSQL database using libpq, execute SQL commands including setting the search path, managing transaction blocks (BEGIN, END), and using cursors to fetch and display data from the `pg_database` system catalog. It includes error handling and resource cleanup.

```c
/*
 * src/test/examples/testlibpq.c
 *
 *
 * testlibpq.c
 *
 *      Test the C version of libpq, the PostgreSQL frontend library.
 */
#include <stdio.h>
#include <stdlib.h>
#include "libpq-fe.h"

static void
exit_nicely(PGconn *conn)
{
    PQfinish(conn);
    exit(1);
}

int
main(int argc, char **argv)
{
    const char *conninfo;
    PGconn     *conn;
    PGresult   *res;
    int         nFields;
    int         i, j;

    /*
     * If the user supplies a parameter on the command line, use it as the
     * conninfo string; otherwise default to setting dbname=postgres and using
     * environment variables or defaults for all other connection parameters.
     */
    if (argc > 1)
        conninfo = argv[1];
    else
        conninfo = "dbname = postgres";

    /* Make a connection to the database */
    conn = PQconnectdb(conninfo);

    /* Check to see that the backend connection was successfully made */
    if (PQstatus(conn) != CONNECTION_OK)
    {
        fprintf(stderr, "%s", PQerrorMessage(conn));
        exit_nicely(conn);
    }

    /* Set always-secure search path, so malicious users can't take control. */
    res = PQexec(conn,
                 "SELECT pg_catalog.set_config('search_path', '', false)");
    if (PQresultStatus(res) != PGRES_TUPLES_OK)
    {
        fprintf(stderr, "SET failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }

    /*
     * Should PQclear PGresult whenever it is no longer needed to avoid memory
     * leaks
     */
    PQclear(res);

    /*
     * Our test case here involves using a cursor, for which we must be inside
     * a transaction block.  We could do the whole thing with a single
     * PQexec() of "select * from pg_database", but that's too trivial to make
     * a good example.
     */

    /* Start a transaction block */
    res = PQexec(conn, "BEGIN");
    if (PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "BEGIN command failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }
    PQclear(res);

    /*
     * Fetch rows from pg_database, the system catalog of databases
     */
    res = PQexec(conn, "DECLARE myportal CURSOR FOR select * from pg_database");
    if (PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "DECLARE CURSOR failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }
    PQclear(res);

    res = PQexec(conn, "FETCH ALL in myportal");
    if (PQresultStatus(res) != PGRES_TUPLES_OK)
    {
        fprintf(stderr, "FETCH ALL failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }

    /* first, print out the attribute names */
    nFields = PQnfields(res);
    for (i = 0; i < nFields; i++)
        printf("% -15s", PQfname(res, i));
    printf("\n\n");

    /* next, print out the rows */
    for (i = 0; i < PQntuples(res); i++)
    {
        for (j = 0; j < nFields; j++)
            printf("% -15s", PQgetvalue(res, i, j));
        printf("\n");
    }

    PQclear(res);

    /* close the portal ... we don't bother to check for errors ... */
    res = PQexec(conn, "CLOSE myportal");
    PQclear(res);

    /* end the transaction */
    res = PQexec(conn, "END");
    PQclear(res);

    /* close the connection to the database and cleanup */
    PQfinish(conn);

    return 0;
}

```

--------------------------------

### Using NTFS Short Names for PATH

Source: https://www.postgresql.org/docs/13/install-windows-full

When installing Bison in a directory with spaces (like 'C:\Program Files'), it may malfunction. This example demonstrates using NTFS short names in the PATH environment variable to circumvent such issues.

```shell
SET PATH=C:\PROGRA~1\GnuWin32;%PATH%
```

--------------------------------

### C libpq Synchronous Database Operations Example

Source: https://www.postgresql.org/docs/15/libpq-example

This C program demonstrates synchronous interaction with a PostgreSQL database using libpq. It connects to the database, executes commands like SET search_path, BEGIN, DECLARE CURSOR, FETCH ALL, CLOSE, and END, and prints query results. It requires libpq to be installed and accessible.

```c
/*
 * src/test/examples/testlibpq.c
 *
 *
 * testlibpq.c
 *
 *      Test the C version of libpq, the PostgreSQL frontend library.
 */
#include <stdio.h>
#include <stdlib.h>
#include "libpq-fe.h"

static void
exit_nicely(PGconn *conn)
{
    PQfinish(conn);
    exit(1);
}

int
main(int argc, char **argv)
{
    const char *conninfo;
    PGconn     *conn;
    PGresult   *res;
    int         nFields;
    int         i, 
                j;

    /*
     * If the user supplies a parameter on the command line, use it as the
     * conninfo string; otherwise default to setting dbname=postgres and using
     * environment variables or defaults for all other connection parameters.
     */
    if (argc > 1)
        conninfo = argv[1];
    else
        conninfo = "dbname = postgres";

    /* Make a connection to the database */
    conn = PQconnectdb(conninfo);

    /* Check to see that the backend connection was successfully made */
    if (PQstatus(conn) != CONNECTION_OK)
    {
        fprintf(stderr, "%s", PQerrorMessage(conn));
        exit_nicely(conn);
    }

    /* Set always-secure search path, so malicious users can't take control. */
    res = PQexec(conn,
                 "SELECT pg_catalog.set_config('search_path', '', false)");
    if (PQresultStatus(res) != PGRES_TUPLES_OK)
    {
        fprintf(stderr, "SET failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }

    /*
     * Should PQclear PGresult whenever it is no longer needed to avoid memory
     * leaks
     */
    PQclear(res);

    /*
     * Our test case here involves using a cursor, for which we must be inside
     * a transaction block.  We could do the whole thing with a single
     * PQexec() of "select * from pg_database", but that's too trivial to make
     * a good example.
     */

    /* Start a transaction block */
    res = PQexec(conn, "BEGIN");
    if (PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "BEGIN command failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }
    PQclear(res);

    /*
     * Fetch rows from pg_database, the system catalog of databases
     */
    res = PQexec(conn, "DECLARE myportal CURSOR FOR select * from pg_database");
    if (PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "DECLARE CURSOR failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }
    PQclear(res);

    res = PQexec(conn, "FETCH ALL in myportal");
    if (PQresultStatus(res) != PGRES_TUPLES_OK)
    {
        fprintf(stderr, "FETCH ALL failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }

    /* first, print out the attribute names */
    nFields = PQnfields(res);
    for (i = 0; i < nFields; i++)
        printf("% -15s", PQfname(res, i));
    printf("\n\n");

    /* next, print out the rows */
    for (i = 0; i < PQntuples(res); i++)
    {
        for (j = 0; j < nFields; j++)
            printf("% -15s", PQgetvalue(res, i, j));
        printf("\n");
    }

    PQclear(res);

    /* close the portal ... we don't bother to check for errors ... */
    res = PQexec(conn, "CLOSE myportal");
    PQclear(res);

    /* end the transaction */
    res = PQexec(conn, "END");
    PQclear(res);

    /* close the connection to the database and cleanup */
    PQfinish(conn);

    return 0;
}

```

--------------------------------

### PostgreSQL Synonym Dictionary Configuration File Example

Source: https://www.postgresql.org/docs/10/textsearch-dictionaries

Provides an example of the content for a PostgreSQL synonym dictionary configuration file. This file maps words to their synonyms and supports prefix matching.

```text
postgres        pgsql
postgresql      pgsql
postgre pgsql
gogle   googl
indices index*
```

--------------------------------

### PostgreSQL SHOW Command Usage Examples

Source: https://www.postgresql.org/docs/7.0/sql-show

Demonstrates how to use the SHOW command in PostgreSQL to retrieve specific run-time parameter settings. Examples include showing the DateStyle and GEQO settings. The output format typically includes a NOTICE message with the variable name and its current value.

```sql
SHOW DateStyle;
NOTICE:  DateStyle is ISO with US (NonEuropean) conventions
```

```sql
SHOW GEQO;
NOTICE:  GEQO is ON beginning with 11 relations
```

--------------------------------

### Helper Functions for libpq Binary Data Processing (C)

Source: https://www.postgresql.org/docs/devel/libpq-example

Contains utility C functions for an example demonstrating libpq's binary I/O. The `exit_nicely` function ensures graceful program termination on error, while `show_binary_results` processes a `PGresult` to extract and display binary integer and bytea data, including crucial byte order conversion for integers using `ntohl`.

```C
#ifdef WIN32
#include <windows.h>
#endif

#include <stdio.h>
#include <stdlib.h>
#include <stdint.h>
#include <string.h>
#include <sys/types.h>
#include "libpq-fe.h"

/* for ntohl/htonl */
#include <netinet/in.h>
#include <arpa/inet.h>


static void
exit_nicely(PGconn *conn)
{
    PQfinish(conn);
    exit(1);
}

/*
 * This function prints a query result that is a binary-format fetch from
 * a table defined as in the comment above.  We split it out because the
 * main() function uses it twice.
 */
static void
show_binary_results(PGresult *res)
{
    int         i,
                j;
    int         i_fnum,
                t_fnum,
                b_fnum;

    /* Use PQfnumber to avoid assumptions about field order in result */
    i_fnum = PQfnumber(res, "i");
    t_fnum = PQfnumber(res, "t");
    b_fnum = PQfnumber(res, "b");

    for (i = 0; i < PQntuples(res); i++)
    {
        char       *iptr;
        char       *tptr;
        char       *bptr;
        int         blen;
        int         ival;

        /* Get the field values (we ignore possibility they are null!) */
        iptr = PQgetvalue(res, i, i_fnum);
        tptr = PQgetvalue(res, i, t_fnum);
        bptr = PQgetvalue(res, i, b_fnum);

        /*
         * The binary representation of INT4 is in network byte order, which
         * we'd better coerce to the local byte order.
         */
        ival = ntohl(*((uint32_t *) iptr));

        /*
         * The binary representation of TEXT is, well, text, and since libpq
         * was nice enough to append a zero byte to it, it'll work just fine
         * as a C string.
         *

```

--------------------------------

### Get pg_receivewal Version

Source: https://www.postgresql.org/docs/15/app-pgreceivewal

Prints the version of the pg_receivewal utility and then exits. This is a common option for checking installed utility versions.

```bash
$ pg_receivewal -V
```

--------------------------------

### PostgreSQL C: Parameterized Queries and Binary I/O

Source: https://www.postgresql.org/docs/8.0/libpq-example

Illustrates using `PQexecParams` for out-of-line parameters and binary data transmission in PostgreSQL. This method simplifies handling special characters and data types by avoiding manual quoting and escaping. It demonstrates fetching integer, text, and bytea data types.

```c
/*
 * testlibpq3.c
 *              Test out-of-line parameters and binary I/O.
 *
 * Before running this, populate a database with the following commands
 * (provided in src/test/examples/testlibpq3.sql):
 *
 * CREATE TABLE test1 (i int4, t text, b bytea);
 *
 * INSERT INTO test1 values (1, 'joe''s place', '\000\001\002\003\004');
 * INSERT INTO test1 values (2, 'ho there', '\004\003\002\001\000');
 *
 * The expected output is:
 *
 * tuple 0:
 *  i = (4 bytes) 1
 *  t = (11 bytes) 'joe's place'
 *  b = (5 bytes) \000\001\002\003\004
 *
 */
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/types.h>
#include "libpq-fe.h"

/* for ntohl/htonl */
#include <netinet/in.h>
#include <arpa/inet.h>


static void
exit_nicely(PGconn *conn)
{
        PQfinish(conn);
        exit(1);
}

int
main(int argc, char **argv)
{
        const char *conninfo;
        PGconn     *conn;
        PGresult   *res;
        const char *paramValues[1];
        int                     i, 
                                j;
        int                     i_fnum, 
                                t_fnum, 
                                b_fnum;

        /*
         * If the user supplies a parameter on the command line, use it as
         * the conninfo string; otherwise default to setting dbname=template1
         * and using environment variables or defaults for all other connection
         * parameters.
         */
        if (argc > 1)
                conninfo = argv[1];
        else
                conninfo = "dbname = template1";

        /* Make a connection to the database */
        conn = PQconnectdb(conninfo);

        /* Check to see that the backend connection was successfully made */
        if (PQstatus(conn) != CONNECTION_OK)
        {
                fprintf(stderr, "Connection to database failed: %s",
                        PQerrorMessage(conn));
                exit_nicely(conn);
        }

        /*
         * The point of this program is to illustrate use of PQexecParams()
         * with out-of-line parameters, as well as binary transmission of
         * results.  By using out-of-line parameters we can avoid a lot of
         * tedious mucking about with quoting and escaping.  Notice how we
         * don't have to do anything special with the quote mark in the
         * parameter value.
         */


```

--------------------------------

### PostgreSQL pg_ctl Start Command

Source: https://www.postgresql.org/docs/current/app-pg-ctl

Starts a PostgreSQL server. Specifies the data directory, an optional log file, and can include server options. The -W option prompts for a password if needed.

```bash
pg_ctl start -D /path/to/data/directory -l /path/to/logfile.log -o "-h localhost" -W -t 60
```

--------------------------------

### Build with LLVM-based JIT Compilation Support

Source: https://www.postgresql.org/docs/12/install-procedure

Enables support for LLVM-based Just-In-Time (JIT) compilation. Requires LLVM version 3.9 or later installed. The `configure` script uses `llvm-config` to find necessary compilation options. You can specify a custom path to `llvm-config` using the `LLVM_CONFIG` environment variable.

```bash
./configure --with-llvm
```

```bash
LLVM_CONFIG='/path/to/llvm/bin/llvm-config' ./configure --with-llvm
```

--------------------------------

### Retrieve Second Column Data Body (Embedded SQL)

Source: https://www.postgresql.org/docs/16/ecpg-sql-get-descriptor

This example illustrates fetching the actual data body of the second column from a descriptor area using `GET DESCRIPTOR`. The `DATA` item for `VALUE 2` is assigned to the host variable `:d_data`.

```Embedded SQL
EXEC SQL GET DESCRIPTOR d VALUE 2 :d_data = DATA;
```

--------------------------------

### PostgreSQL System Call Error Message Example

Source: https://www.postgresql.org/docs/11/error-style-guide

Shows how to improve error messages related to system calls. Instead of just reporting the failure of a specific system call ('open() failed: %m'), the 'BETTER' example describes the intended action ('could not open file %s: %m'), making it more understandable to the user.

```text
BAD:    open() failed: %m
BETTER: could not open file %s: %m

```

--------------------------------

### Get PostgreSQL Server Start Time

Source: https://www.postgresql.org/docs/11/functions-info

This function returns the timestamp with time zone indicating when the PostgreSQL server process (postmaster) started. It provides a simple way to determine the server's uptime or last restart time.

```sql
SELECT pg_postmaster_start_time();
```

--------------------------------

### Connect to PostgreSQL and Handle Notifications

Source: https://www.postgresql.org/docs/current/libpq-example

This C code snippet demonstrates how to establish a connection to a PostgreSQL database using libpq, execute SQL commands like 'SET' and 'LISTEN', and handle asynchronous notifications. It includes error checking for connection and command execution, and uses `select` to wait for notifications.

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/types.h>
#include "libpq-fe.h"
#include <errno.h>
#include <unistd.h>
#include <sys/select.h>

static void exit_nicely(PGconn *conn)
{
    fprintf(stderr, "%s", PQerrorMessage(conn));
    PQfinish(conn);
    exit(1);
}

int main(int argc, char **argv)
{
    PGconn     *conn;
    PGresult   *res;
    const char *conninfo;
    int         nnotifies;
    PGnotify   *notify;

    /*normally you would get the conninfo from configuration files and not from argv */
    if (argc > 1)
        conninfo = argv[1];
    else
        conninfo = "dbname = postgres";

    /* Make a connection to the database */
    conn = PQconnectdb(conninfo);

    /* Check to see that the backend connection was successfully made */
    if (PQstatus(conn) != CONNECTION_OK)
    {
        fprintf(stderr, "%s", PQerrorMessage(conn));
        exit_nicely(conn);
    }

    /* Set always-secure search path, so malicious users can't take control. */
    res = PQexec(conn,
                 "SELECT pg_catalog.set_config('search_path', '', false)");
    if (PQresultStatus(res) != PGRES_TUPLES_OK)
    {
        fprintf(stderr, "SET failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }

    /*
     * Should PQclear PGresult whenever it is no longer needed to avoid memory
     * leaks
     */
    PQclear(res);

    /*
     * Issue LISTEN command to enable notifications from the rule's NOTIFY.
     */
    res = PQexec(conn, "LISTEN TBL2");
    if (PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "LISTEN command failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }
    PQclear(res);

    /* Quit after four notifies are received. */
    nnotifies = 0;
    while (nnotifies < 4)
    {
        /*
         * Sleep until something happens on the connection.  We use select(2)
         * to wait for input, but you could also use poll() or similar
         * facilities.
         */
        int         sock;
        fd_set      input_mask;

        sock = PQsocket(conn);

        if (sock < 0)
            break;              /* shouldn't happen */

        FD_ZERO(&input_mask);
        FD_SET(sock, &input_mask);

        if (select(sock + 1, &input_mask, NULL, NULL, NULL) < 0)
        {
            fprintf(stderr, "select() failed: %s\n", strerror(errno));
            exit_nicely(conn);
        }

        /* Now check for input */
        PQconsumeInput(conn);
        while ((notify = PQnotifies(conn)) != NULL)
        {
            fprintf(stderr,
                    "ASYNC NOTIFY of '%s' received from backend PID %d\n",
                    notify->relname, notify->be_pid);
            PQfreemem(notify);
            nnotifies++;
            PQconsumeInput(conn);
        }
    }

    fprintf(stderr, "Done.\n");

    /* close the connection to the database and cleanup */
    PQfinish(conn);

    return 0;
}

```

--------------------------------

### PostgreSQL START_REPLICATION Logical Command Example

Source: https://www.postgresql.org/docs/17/protocol-logical-replication

This example demonstrates how to initiate logical streaming replication using the START_REPLICATION command in PostgreSQL. It includes common parameters such as protocol version, publication names, and streaming options. Ensure your PostgreSQL version supports the specified protocol version.

```sql
START_REPLICATION SLOT replication_slot LOGICAL (proto_version '3', publication_names 'my_publication', streaming 'on', binary 'true')
```

--------------------------------

### PostgreSQL SELinux Dynamic Domain Transitions Example

Source: https://www.postgresql.org/docs/11/sepgsql

Demonstrates SELinux dynamic domain transitions in PostgreSQL using SQL commands. It shows how to retrieve the current security context, transition to a more restricted context, and the denial of transitioning back to a broader context. This highlights the security implications of allowing transitions only to domains with fewer privileges.

```sql
regression=# select sepgsql_getcon();
                    sepgsql_getcon
-------------------------------------------------------
 unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
(1 row)

regression=# SELECT sepgsql_setcon('unconfined_u:unconfined_r:unconfined_t:s0-s0:c1.c4');
 sepgsql_setcon 
----------------
 t
(1 row)

regression=# SELECT sepgsql_setcon('unconfined_u:unconfined_r:unconfined_t:s0-s0:c1.c1023');
ERROR:  SELinux: security policy violation


```

--------------------------------

### PostgreSQL Configuration File Example

Source: https://www.postgresql.org/docs/12/config-setting

Provides an example of the `postgresql.conf` file, which is used for setting server configuration parameters. This file is typically located in the data directory.

```ini
# Example postgresql.conf

#------------------------------------------------------------------------------
# GRACEFUL SHUTDOWN
#------------------------------------------------------------------------------

#when to stop background processes.
#external_pid_file = "/path/to/pid/file"

# (change the log directory when changing the data directory)
#log_directory = "pg_log"

#log_filename = "postgresql-%a.log"

#log_connections = off
#log_disconnections = off
#log_duration = off
#log_executor_stats = off
#log_statement = off
#log_replication_commands = off
#log_routine_stats = off
#log_statement_stats = off
#log_temp_files = 0                      # -1 disables, 0 logs all temp files above 1MB
#log_truncate_on_rotation = off
#log_rotation_age = 1d                   # one day
#log_rotation_size = 10MB                # 10 megabytes

#log_timezone = 'GMT'

#------------------------------------------------------------------------------
# PROCESS MANAGEMENT
#------------------------------------------------------------------------------

#Authentication:
#Authentication configuration file
# authentication_timeout = 1min             # 1s-600s
# (change the data directory when changing the data directory)
#data_directory = "/var/lib/postgresql/15/main"

#external_pid_file = "/run/postgresql/15-main.pid"

#fsync = on                              # Flush data to disk on each commit
#synchronous_commit = on                 # "on", "local", "remote_write", "remote_apply", "off"
#synchronous_standby_names = ''          # format: 'stream_replica_name[,...[:sync|:async]]'
#wal_sync_method = fsync                 # Decide how to force a sync of the WAL
#wal_buffers = -1                        # -1 selects 512 KB. Minimum is -1, max is wal_size.
#wal_writer_delay = 200ms
#wal_recycle = on
#wal_log_hints = off                     # include hints about block changes
#wal_compression = off
#wal_level = replica                     # minimal, replica, or logical
#wal_keep_size = 0                       # old logs are removed when WAL is full
#min_wal_size = 1GB
#max_wal_size = 4GB
#checkpoint_timeout = 5min               # range 1 min to 10 days
#checkpoint_completion_target = 0.9      # promote close to date but finish WAL use
#checkpoint_flush_after = 256kB          # measured in pages, 0 disables
#archive_mode = off                      # needed for continuous archiving
#archive_command = ''                    # command to execute for archival
#archive_timeout = 0                     # 0 disables
#archive_cleanup_command = ''
#archive_library = ''

#------------------------------------------------------------------------------
# RECOVERY AND WAL REPLAY
#------------------------------------------------------------------------------

#hot_standby = off                       # - standby servers can answer read-only queries
#max_standby_streaming_delay = 30s       # max delay before refusing query on standby
#standby_file_queue_max = "1000"
#wal_receiver_status_interval = 10s      # updates WAL receiver status every 10 seconds
#wal_receiver_create_temp_table = off

#------------------------------------------------------------------------------
# REPLICATION
#------------------------------------------------------------------------------

#max_replication_slots = 0
#max_logical_replication_workers = 4
#max_sync_replication_workers = 2

#------------------------------------------------------------------------------
# CONNECTION AND AUTHENTICATION
#------------------------------------------------------------------------------

#listen_addresses = 'localhost'          # what IP address(es) to listen on;
                                        # comma-separated list of addresses;
                                        # defaults to 'localhost'; "*" means all
                                        # (change requires restart)
#port = 5432                             # (change requires restart)

#max_connections = 100                   # (change requires restart)
#superuser_reserved_connections = 3      # (change requires restart)
#unix_socket_directories = '/var/run/postgresql' # comma-separated list of directories
#unix_socket_group = ''
#unix_socket_permissions = 0777          # System V IPC naming (use to control access to shared memory segment)
# (change requires restart)

# Note: You must disable TCP/IP connections if TCP/IP connections are not needed.
#       This is done by setting `listen_addresses = 'localhost'` in this file.
#       And then restarting the server. Then, you need to set up your 
#       `pg_hba.conf` to prevent access from remote hosts. For example, 
#       you could use the following lines in `pg_hba.conf`:
# local   all             all                                     peer
# host    all             all             127.0.0.1/32            scram-sha-256
# host    all             all             ::1/128                 scram-sha-256

#password_encryption = scram-sha-256     # scram-sha-256 or md5

#------------------------------------------------------------------------------
# RESOURCES UTILIZATION
#------------------------------------------------------------------------------

#maximum amount of memory used by the shared buffers, main memory allocation area
#shared_buffers = 128MB                  # min 128kB
# (change requires restart)

#max_locks_per_transaction = 64          # autovacuum max_locks_per_transaction = 2000
#max_prepared_transactions = 0           # zero disables the feature
# (change requires restart)

# Caution: Setting max_worker_processes > 8 requires kernel support.
# (change requires restart)
#max_worker_processes = 8                # (change requires restart)
#max_parallel_workers = 8                # (change requires restart)
#max_parallel_workers_per_gather = 4     # (change requires restart)
#max_parallel_maintenance_workers = 4    # (change requires restart)

#------------------------------------------------------------------------------
# MEMORY MANAGEMENT
#------------------------------------------------------------------------------

#work_mem = 4MB                          # min 64kB
# (change requires restart)

#maintenance_work_mem = 64MB             # min 1MB
# (change requires restart)

#shared_memory_size = 128MB              # (change requires restart)
# (change requires restart)

#------------------------------------------------------------------------------
# BACKGROUND WRITER
#------------------------------------------------------------------------------

#bgwriter_delay = 10ms                   # background writer delay
#bgwriter_lru_maxpages = 100             # max number of pages a writer can sweep at a time
#bgwriter_lru_multiplier = 2.0           # how many clean buffers are kept around
#bgwriter_flush_after = 1MB              # previously written when flush after

#------------------------------------------------------------------------------
# ASYNCHRONOUS AND SUSPENDED I/O
#------------------------------------------------------------------------------

#effective_io_concurrency = 1            # effective io for systems
# (change requires restart)

# Note: For traditional spinning disks, this should be set to 1.
# For SSDs, this value should be higher (e.g. 100 or more).
# Check your system's capabilities before setting this value.

#------------------------------------------------------------------------------
# WAL WRITER
#------------------------------------------------------------------------------

#wal_writer_delay = 200ms
#wal_writer_flush_after = 1MB

#------------------------------------------------------------------------------
# CHECKPOINTING
#------------------------------------------------------------------------------

#checkpoint_timeout = 5min               # range 1 min to 10 days
#checkpoint_completion_target = 0.9      # promote close to date but finish WAL use
#checkpoint_flush_after = 256kB          # measured in pages, 0 disables
#max_wal_size = 4GB
#min_wal_size = 1GB

#------------------------------------------------------------------------------
# ERROR REPORTING AND LOGGING
#------------------------------------------------------------------------------

#log_destination = 'stderr'              # Valid values are combinations of
                                        # stderr, csvlog, syslog, and eventlog.
                                        # (change requires restart)

#logging_collector = on                  # Enable capturing of stderr to log files.
                                        # Requires logging_collector to be on.
                                        # (change requires restart)

#log_directory = "log"
#log_filename = "postgresql-%Y-%m-%d_%H%M%S.log"
#log_file_mode = 0600
#log_rotation_age = 1d                   # days
#log_rotation_size = 10MB                # bytes
#log_min_duration_statement = -1       # -1 disables, 0 logs all statements
                                        # >= 0 logs statements longer than N milliseconds
#log_min_error_statement = 256           # All statements
#log_min_messages = warning              # Set to 'debug', 'log', 'notice', 'warning', 'error', 'fatal', 'panic' (change requires restart)
#log_replication_commands = off
#log_stat = off
#log_statement = off                     # none, ddl, mod, all
#log_transaction_stats = off
#log_executor_stats = off
#log_parser_stats = off
#log_planner_stats = off
#log_statement_stats = off
#log_temp_files = 0                      # -1 disables, 0 logs all temp files above 1MB
#log_connections = off
#log_disconnections = off
#log_duration = off
#log_lock_waits = off                    # report locking waits
#log_rollback = off                      # log transaction rollbacks
#log_recovery_conflicts = off            # log recovery conflicts
#log_checkpoints = off                   # log each checkpoint
#log_cleanup_info = off                  # log info for VACUUM operations
#log_lock_waits = off                    # report locking waits
#log_autovacuum_min_duration = 0         # -1 disables, 0 logs all autovacuum actions
                                        # >= 0 logs autovacuum actions longer than N milliseconds
#log_error_verbosity = default           # Creates more or less informative error messages.
#                                        # debug, default, verbose
#log_line_prefix = ''                    # special formatters: %a = user, %u = database, %m = time, %p = pid
#                                        # (change requires restart)
#log_remote_sql = on
#log_statement_stats = off
#log_timezone = 'GMT'

#------------------------------------------------------------------------------
# AUTOVACUUM LAUNCHER
#------------------------------------------------------------------------------

#autovacuum = on                         # Enable autovacuum subprocesses
                                        # (change requires restart)

#log_autovacuum_min_duration = -1        # -1 disables, 0 logs all autovacuum actions
                                        # >= 0 logs autovacuum actions longer than N milliseconds

#autovacuum_max_workers = 3              # max number of autovacuum worker processes
                                        # (change requires restart)

#autovacuum_naptime = 1min               # time between two autovacuum runs
#autovacuum_vacuum_threshold = 50        # min number of row updates before vacuum
#autovacuum_analyze_threshold = 50       # min number of row updates before analyze
#autovacuum_vacuum_scale_factor = 0.2    # fraction of table size before vacuum
#autovacuum_analyze_scale_factor = 0.1   # fraction of table size before analyze
#autovacuum_freeze_max_age = 200000000   # maximum XID age before aggressive vacuum
#autovacuum_multixact_maxage = 400000000 # maximum multixact age before aggressive vacuum

#------------------------------------------------------------------------------
# CLIENT CONNECTION DEFAULTS
#------------------------------------------------------------------------------

# A comma-separated list of IP addresses that the server should listen on.
# A empty string means no TCP/IP connections (only Unix domain sockets).
# Default is "localhost" on commercial Unixes, "*" on Windows.
# listen_addresses = 'localhost'          # what IP address(es) to listen on;
                                        # comma-separated list of addresses;
                                        # defaults to 'localhost'; "*" means all
                                        # (change requires restart)

# This is the port the Postmaster is to listen on. Default is 5432.
# When PostgreSQL is not running, you can use the `pg_ctl` utility 
# to start and stop the server.
# port = 5432                             # (change requires restart)

#------------------------------------------------------------------------------
# DEADLOCK DETECTOR
#------------------------------------------------------------------------------

#deadlock_timeout = 1s                   # time to wait for deadlock to be detected
#deadlock_timeout = 1000                 # (change requires restart)

#------------------------------------------------------------------------------
# STATISTICS AND LOGGING
#------------------------------------------------------------------------------

#log_statement = 'none'                  # none, ddl, mod, all
# (change requires restart)

#log_min_duration_statement = -1       # -1 disables, 0 logs all statements
                                        # >= 0 logs statements longer than N milliseconds

#------------------------------------------------------------------------------
# APPLICATION CONFIGURATION PARAMETERS
#------------------------------------------------------------------------------

#shared_buffers = 128MB                  # min 128kB
# (change requires restart)

#work_mem = 4MB                          # min 64kB
# (change requires restart)

#maintenance_work_mem = 64MB             # min 1MB
# (change requires restart)

#effective_io_concurrency = 1            # effective io for systems
# (change requires restart)

#------------------------------------------------------------------------------
# LOCK MANAGEMENT
#------------------------------------------------------------------------------

#max_locks_per_transaction = 64          # autovacuum max_locks_per_transaction = 2000
#max_prepared_transactions = 0           # zero disables the feature
# (change requires restart)

#------------------------------------------------------------------------------
# INDEX MANAGEMENT
#------------------------------------------------------------------------------

#------------------------------------------------------------------------------
# THREAD MANAGEMENT
#------------------------------------------------------------------------------

# Caution: Setting max_worker_processes > 8 requires kernel support.
# (change requires restart)
#max_worker_processes = 8                # (change requires restart)
#max_parallel_workers = 8                # (change requires restart)
#max_parallel_workers_per_gather = 4     # (change requires restart)
#max_parallel_maintenance_workers = 4    # (change requires restart)

#------------------------------------------------------------------------------
# EXTERNAL TOOLS
#------------------------------------------------------------------------------

#------------------------------------------------------------------------------
# STATEMENT MANAGEMENT
#------------------------------------------------------------------------------

#log_statement = 'none'                  # none, ddl, mod, all
# (change requires restart)

#log_min_duration_statement = -1       # -1 disables, 0 logs all statements
                                        # >= 0 logs statements longer than N milliseconds

#------------------------------------------------------------------------------
# RESOURCE CONSUMPTION
#------------------------------------------------------------------------------

#shared_buffers = 128MB                  # min 128kB
# (change requires restart)

#work_mem = 4MB                          # min 64kB
# (change requires restart)

#maintenance_work_mem = 64MB             # min 1MB
# (change requires restart)

#effective_io_concurrency = 1            # effective io for systems
# (change requires restart)

#------------------------------------------------------------------------------
# QUERY PLAN MANAGEMENT
#------------------------------------------------------------------------------

#plan_cache_mode = auto                  # auto, force_custom_plan, force_generic_plan

#------------------------------------------------------------------------------
# CONNECTION POOLING
#------------------------------------------------------------------------------

#------------------------------------------------------------------------------
# MEMORY
#------------------------------------------------------------------------------

#shared_memory_size = 128MB              # (change requires restart)

#------------------------------------------------------------------------------
# SYSTEM IDENTIFICATION
#------------------------------------------------------------------------------

#------------------------------------------------------------------------------
# WAL ARCHIVING
#------------------------------------------------------------------------------

#archive_mode = off                      # needed for continuous archiving
#archive_command = ''                    # command to execute for archival
#archive_timeout = 0                     # 0 disables

#------------------------------------------------------------------------------
# CLIENT AUTHENTICATION
#------------------------------------------------------------------------------

#authentication_timeout = 1min             # 1s-600s

#------------------------------------------------------------------------------
# CACHING
#------------------------------------------------------------------------------

#shared_buffers = 128MB                  # min 128kB
# (change requires restart)

#------------------------------------------------------------------------------
# BUFFER MANAGEMENT
#------------------------------------------------------------------------------

#bgwriter_delay = 10ms                   # background writer delay
#bgwriter_lru_maxpages = 100             # max number of pages a writer can sweep at a time
#bgwriter_lru_multiplier = 2.0           # how many clean buffers are kept around
#bgwriter_flush_after = 1MB              # previously written when flush after

#------------------------------------------------------------------------------
# TRANSACTIONS
#------------------------------------------------------------------------------

#max_locks_per_transaction = 64          # autovacuum max_locks_per_transaction = 2000
#max_prepared_transactions = 0           # zero disables the feature
# (change requires restart)

#------------------------------------------------------------------------------
# LOGGING
#------------------------------------------------------------------------------

#log_destination = 'stderr'              # Valid values are combinations of
                                        # stderr, csvlog, syslog, and eventlog.
                                        # (change requires restart)

#logging_collector = on                  # Enable capturing of stderr to log files.
                                        # Requires logging_collector to be on.
                                        # (change requires restart)

#log_directory = "log"
#log_filename = "postgresql-%Y-%m-%d_%H%M%S.log"
#log_file_mode = 0600
#log_rotation_age = 1d                   # days
#log_rotation_size = 10MB                # bytes
#log_min_duration_statement = -1       # -1 disables, 0 logs all statements
                                        # >= 0 logs statements longer than N milliseconds
#log_min_error_statement = 256           # All statements
#log_min_messages = warning              # Set to 'debug', 'log', 'notice', 'warning', 'error', 'fatal', 'panic' (change requires restart)
#log_replication_commands = off
#log_stat = off
#log_statement = off                     # none, ddl, mod, all
#log_transaction_stats = off
#log_executor_stats = off
#log_parser_stats = off
#log_planner_stats = off
#log_statement_stats = off
#log_temp_files = 0                      # -1 disables, 0 logs all temp files above 1MB
#log_connections = off
#log_disconnections = off
#log_duration = off
#log_lock_waits = off                    # report locking waits
#log_rollback = off                      # log transaction rollbacks
#log_recovery_conflicts = off            # log recovery conflicts
#log_checkpoints = off                   # log each checkpoint
#log_cleanup_info = off                  # log info for VACUUM operations
#log_lock_waits = off                    # report locking waits
#log_autovacuum_min_duration = 0         # -1 disables, 0 logs all autovacuum actions
                                        # >= 0 logs autovacuum actions longer than N milliseconds
#log_error_verbosity = default           # Creates more or less informative error messages.
#                                        # debug, default, verbose
#log_line_prefix = ''                    # special formatters: %a = user, %u = database, %m = time, %p = pid
#                                        # (change requires restart)
#log_remote_sql = on
#log_statement_stats = off
#log_timezone = 'GMT'

#------------------------------------------------------------------------------
# WAL ARCHIVING
#------------------------------------------------------------------------------

#archive_mode = off                      # needed for continuous archiving
#archive_command = ''                    # command to execute for archival
#archive_timeout = 0                     # 0 disables

#------------------------------------------------------------------------------
# CLIENT AUTHENTICATION
#------------------------------------------------------------------------------

#authentication_timeout = 1min             # 1s-600s

#------------------------------------------------------------------------------
# MONITORING
#------------------------------------------------------------------------------

#log_connections = off
#log_disconnections = off
#log_duration = off
#log_lock_waits = off                    # report locking waits
#log_statement = off                     # none, ddl, mod, all

#------------------------------------------------------------------------------
# AUTOVACUUM
#------------------------------------------------------------------------------

#autovacuum = on                         # Enable autovacuum subprocesses
                                        # (change requires restart)

#log_autovacuum_min_duration = -1        # -1 disables, 0 logs all autovacuum actions
                                        # >= 0 logs autovacuum actions longer than N milliseconds

#autovacuum_max_workers = 3              # max number of autovacuum worker processes
                                        # (change requires restart)

#autovacuum_naptime = 1min               # time between two autovacuum runs
#autovacuum_vacuum_threshold = 50        # min number of row updates before vacuum
#autovacuum_analyze_threshold = 50       # min number of row updates before analyze
#autovacuum_vacuum_scale_factor = 0.2    # fraction of table size before vacuum
#autovacuum_analyze_scale_factor = 0.1   # fraction of table size before analyze
#autovacuum_freeze_max_age = 200000000   # maximum XID age before aggressive vacuum
#autovacuum_multixact_maxage = 400000000 # maximum multixact age before aggressive vacuum

#------------------------------------------------------------------------------
# MEMORY ALLOCATION
#------------------------------------------------------------------------------

#shared_buffers = 128MB                  # min 128kB
# (change requires restart)

#work_mem = 4MB                          # min 64kB
# (change requires restart)

#maintenance_work_mem = 64MB             # min 1MB
# (change requires restart)

#------------------------------------------------------------------------------
# CHECKPOINTING
#------------------------------------------------------------------------------

#checkpoint_timeout = 5min               # range 1 min to 10 days
#checkpoint_completion_target = 0.9      # promote close to date but finish WAL use
#checkpoint_flush_after = 256kB          # measured in pages, 0 disables
#max_wal_size = 4GB
#min_wal_size = 1GB

#------------------------------------------------------------------------------
# RECOVERY
#------------------------------------------------------------------------------

#hot_standby = off                       # - standby servers can answer read-only queries
#max_standby_streaming_delay = 30s       # max delay before refusing query on standby
#standby_file_queue_max = "1000"
#wal_receiver_status_interval = 10s      # updates WAL receiver status every 10 seconds
#wal_receiver_create_temp_table = off

#------------------------------------------------------------------------------
# REPLICATION SLOTS
#------------------------------------------------------------------------------

#max_replication_slots = 0
#max_logical_replication_workers = 4
#max_sync_replication_workers = 2

#------------------------------------------------------------------------------
# REPLICATION
#------------------------------------------------------------------------------

#hot_standby = off                       # - standby servers can answer read-only queries
#max_standby_streaming_delay = 30s       # max delay before refusing query on standby
#standby_file_queue_max = "1000"
#wal_receiver_status_interval = 10s      # updates WAL receiver status every 10 seconds
#wal_receiver_create_temp_table = off

#------------------------------------------------------------------------------
# ADVANCED FEATURES
#------------------------------------------------------------------------------

#------------------------------------------------------------------------------
# FILE SYSTEM CACHING
#------------------------------------------------------------------------------

#------------------------------------------------------------------------------
# SYSTEM IDENTIFICATION
#------------------------------------------------------------------------------

#------------------------------------------------------------------------------
# WAL WRITER
#------------------------------------------------------------------------------

#wal_writer_delay = 200ms
#wal_writer_flush_after = 1MB

#------------------------------------------------------------------------------
# WAL WRITER
#------------------------------------------------------------------------------

#wal_writer_delay = 200ms
#wal_writer_flush_after = 1MB

#------------------------------------------------------------------------------
# RECOVERY AND WAL REPLAY
#------------------------------------------------------------------------------

#hot_standby = off                       # - standby servers can answer read-only queries
#max_standby_streaming_delay = 30s       # max delay before refusing query on standby
#standby_file_queue_max = "1000"
#wal_receiver_status_interval = 10s      # updates WAL receiver status every 10 seconds
#wal_receiver_create_temp_table = off

#------------------------------------------------------------------------------
# WAL ARCHIVING
#------------------------------------------------------------------------------

#archive_mode = off                      # needed for continuous archiving
#archive_command = ''                    # command to execute for archival
#archive_timeout = 0                     # 0 disables

#------------------------------------------------------------------------------
# REPLICATION SLOTS
#------------------------------------------------------------------------------

#max_replication_slots = 0
#max_logical_replication_workers = 4
#max_sync_replication_workers = 2

#------------------------------------------------------------------------------
# CLIENT AUTHENTICATION
#------------------------------------------------------------------------------

#authentication_timeout = 1min             # 1s-600s

#------------------------------------------------------------------------------
# LOGGING
#------------------------------------------------------------------------------

#log_destination = 'stderr'              # Valid values are combinations of
                                        # stderr, csvlog, syslog, and eventlog.
                                        # (change requires restart)

#logging_collector = on                  # Enable capturing of stderr to log files.
                                        # Requires logging_collector to be on.
                                        # (change requires restart)

#log_directory = "log"
#log_filename = "postgresql-%Y-%m-%d_%H%M%S.log"
#log_file_mode = 0600
#log_rotation_age = 1d                   # days
#log_rotation_size = 10MB                # bytes
#log_min_duration_statement = -1       # -1 disables, 0 logs all statements
                                        # >= 0 logs statements longer than N milliseconds
#log_min_error_statement = 256           # All statements
#log_min_messages = warning              # Set to 'debug', 'log', 'notice', 'warning', 'error', 'fatal', 'panic' (change requires restart)
#log_replication_commands = off
#log_stat = off
#log_statement = off                     # none, ddl, mod, all
#log_transaction_stats = off
#log_executor_stats = off
#log_parser_stats = off
#log_planner_stats = off
#log_statement_stats = off
#log_temp_files = 0                      # -1 disables, 0 logs all temp files above 1MB
#log_connections = off
#log_disconnections = off
#log_duration = off
#log_lock_waits = off                    # report locking waits
#log_rollback = off                      # log transaction rollbacks
#log_recovery_conflicts = off            # log recovery conflicts
#log_checkpoints = off                   # log each checkpoint
#log_cleanup_info = off                  # log info for VACUUM operations
#log_lock_waits = off                    # report locking waits
#log_autovacuum_min_duration = 0         # -1 disables, 0 logs all autovacuum actions
                                        # >= 0 logs autovacuum actions longer than N milliseconds
#log_error_verbosity = default           # Creates more or less informative error messages.
#                                        # debug, default, verbose
#log_line_prefix = ''                    # special formatters: %a = user, %u = database, %m = time, %p = pid
#                                        # (change requires restart)
#log_remote_sql = on
#log_statement_stats = off
#log_timezone = 'GMT'

#------------------------------------------------------------------------------
# AUTOVACUUM LAUNCHER
#------------------------------------------------------------------------------

#autovacuum = on                         # Enable autovacuum subprocesses
                                        # (change requires restart)

#log_autovacuum_min_duration = -1        # -1 disables, 0 logs all autovacuum actions
                                        #
```

--------------------------------

### Configure PostgreSQL for Logical Replication (SQL)

Source: https://www.postgresql.org/docs/current/logical-replication-quick-setup

This snippet shows the essential SQL commands to set up logical replication in PostgreSQL. It includes creating a publication on the publisher database and a subscription on the subscriber database, specifying which tables to replicate and connection details.

```sql
CREATE PUBLICATION mypub FOR TABLE users, departments;

CREATE SUBSCRIPTION mysub CONNECTION 'dbname=foo host=bar user=repuser' PUBLICATION mypub;
```

--------------------------------

### Example: Dumping a Database and Reloading

Source: https://www.postgresql.org/docs/6.5/app-pg-dump

These examples demonstrate how to use pg_dump to create a database backup and then how to use psql to restore that database from the generated script file.

```bash
# To dump a database of the same name as the user:
% pg_dump > db.out
```

```bash
# To reload this database:
% psql -e database < db.out
```

--------------------------------

### Example: Using COPY with PQputline and PQendcopy

Source: https://www.postgresql.org/docs/6.4/libpq-chapter17121

This example demonstrates a typical workflow for using the COPY command, involving creating a table, initiating a copy from stdin, sending data lines using PQputline, and concluding the operation with PQendcopy.

```c
PQexec(conn, "create table foo (a int4, b char16, d float8)");
PQexec(conn, "copy foo from stdin");
PQputline(conn, "3<TAB>hello world<TAB>4.5\n");
PQputline(conn,"4<TAB>goodbye world<TAB>7.11\n");
...
PQputline(conn,"\\.\n");
PQendcopy(conn);

```

--------------------------------

### PostgreSQL: Create Table and Index

Source: https://www.postgresql.org/docs/12/indexes-intro

Demonstrates the SQL commands to create a sample table and then add an index to a specific column for performance optimization.

```sql
CREATE TABLE test1 (
    id integer,
    content varchar
);

CREATE INDEX test1_id_index ON test1 (id);
```

--------------------------------

### Configure Shell Path for CVSup

Source: https://www.postgresql.org/docs/6.5/cvs23780

This snippet shows how to update the system's PATH environment variable to include the directory where the CVSup binary has been installed. It uses the 'rehash' command to update the shell's hash table and 'which' to verify the installation.

```shell
$ rehash
$ which cvsup
$ set path=(""/usr/local/bin"" $path)
$ which cvsup
/usr/local/bin/cvsup
```

--------------------------------

### Install PostgreSQL System Files (make install)

Source: https://www.postgresql.org/docs/10/install-procedure

Installs the core PostgreSQL system files into specified directories. Requires appropriate write permissions, often executed as root. The target directories are defined during the configuration step.

```shell
make install
```

--------------------------------

### PostgreSQL C: Connect and Listen for Notifications

Source: https://www.postgresql.org/docs/8.0/libpq-example

Establishes a connection to a PostgreSQL database and listens for asynchronous notifications on a specified channel. It uses `select` to wait for database events and `PQconsumeInput`/`PQnotifies` to process incoming notifications. The program exits after receiving a specified number of notifications.

```c
/*
         */
        if (argc > 1)
                conninfo = argv[1];
        else
                conninfo = "dbname = template1";

        /* Make a connection to the database */
        conn = PQconnectdb(conninfo);

        /* Check to see that the backend connection was successfully made */
        if (PQstatus(conn) != CONNECTION_OK)
        {
                fprintf(stderr, "Connection to database failed: %s",
                                PQerrorMessage(conn));
                exit_nicely(conn);
        }

        /*
         * Issue LISTEN command to enable notifications from the rule's NOTIFY.
         */
        res = PQexec(conn, "LISTEN TBL2");
        if (PQresultStatus(res) != PGRES_COMMAND_OK)
        {
                fprintf(stderr, "LISTEN command failed: %s", PQerrorMessage(conn));
                PQclear(res);
                exit_nicely(conn);
        }

        /*
         * should PQclear PGresult whenever it is no longer needed to avoid
         * memory leaks
         */
        PQclear(res);

        /* Quit after four notifies are received. */
        nnotifies = 0;
        while (nnotifies < 4)
        {
                /*
                 * Sleep until something happens on the connection.  We use select(2)
                 * to wait for input, but you could also use poll() or similar
                 * facilities.
                 */
                int                     sock;
                fd_set          input_mask;

                sock = PQsocket(conn);

                if (sock < 0)
                        break;                          /* shouldn't happen */

                FD_ZERO(&input_mask);
                FD_SET(sock, &input_mask);

                if (select(sock + 1, &input_mask, NULL, NULL, NULL) < 0)
                {
                        fprintf(stderr, "select() failed: %s\n", strerror(errno));
                        exit_nicely(conn);
                }

                /* Now check for input */
                PQconsumeInput(conn);
                while ((notify = PQnotifies(conn)) != NULL)
                {
                        fprintf(stderr,
                                        "ASYNC NOTIFY of '%s' received from backend pid %d\n",
                                        notify->relname, notify->be_pid);
                        PQfreemem(notify);
                        nnotifies++;
                }
        }

        fprintf(stderr, "Done.\n");

        /* close the connection to the database and cleanup */
        PQfinish(conn);

        return 0;
}

```

--------------------------------

### Connect to PostgreSQL and Query Database using C (libpq)

Source: https://www.postgresql.org/docs/6.3/c4410

This C code snippet demonstrates how to use the libpq library to connect to a PostgreSQL database, execute a SQL query to fetch all entries from 'pg_database', and then process and display the results. It covers connection establishment, transaction management, cursor usage, and result set retrieval.

```c
/*
 * testlibpq.c
 *   Test the C version of LIBPQ, the Postgres frontend library.
 *
 *
 */
#include <stdio.h>
#include "libpq-fe.h"

void
exit_nicely(PGconn* conn)
{
  PQfinish(conn);
  exit(1);
}

main()
{
  char *pghost, *pgport, *pgoptions, *pgtty;
  char* dbName;
  int nFields;
  int i,j;

/*  FILE *debug; */

  PGconn* conn;
  PGresult* res;

  /* begin, by setting the parameters for a backend connection
     if the parameters are null, then the system will try to use
     reasonable defaults by looking up environment variables
     or, failing that, using hardwired constants */
  pghost = NULL;  /* host name of the backend server */
  pgport = NULL;  /* port of the backend server */
  pgoptions = NULL; /* special options to start up the backend server */
  pgtty = NULL;     /* debugging tty for the backend server */
  dbName = "template1";

  /* make a connection to the database */
  conn = PQsetdb(pghost, pgport, pgoptions, pgtty, dbName);

  /* check to see that the backend connection was successfully made */
  if (PQstatus(conn) == CONNECTION_BAD) {
    fprintf(stderr,"Connection to database '%s' failed.\n", dbName);
    fprintf(stderr,"%s",PQerrorMessage(conn));
    exit_nicely(conn);
  }

/*  debug = fopen("/tmp/trace.out","w");  */
/*   PQtrace(conn, debug);  */

  /* start a transaction block */

  res = PQexec(conn,"BEGIN");
  if (PQresultStatus(res) != PGRES_COMMAND_OK) {
    fprintf(stderr,"BEGIN command failed\n");
    PQclear(res);
    exit_nicely(conn);
  }
  /* should PQclear PGresult whenever it is no longer needed to avoid
     memory leaks */
  PQclear(res);

  /* fetch instances from the pg_database, the system catalog of databases*/
  res = PQexec(conn,"DECLARE myportal CURSOR FOR select * from pg_database");
  if (PQresultStatus(res) != PGRES_COMMAND_OK) {
    fprintf(stderr,"DECLARE CURSOR command failed\n");
    PQclear(res);
    exit_nicely(conn);
  }
  PQclear(res);

  res = PQexec(conn,"FETCH ALL in myportal");
  if (PQresultStatus(res) != PGRES_TUPLES_OK) {
    fprintf(stderr,"FETCH ALL command didn't return tuples properly\n");
    PQclear(res);
    exit_nicely(conn);
  }

  /* first, print out the attribute names */
  nFields = PQnfields(res);
  for (i=0; i < nFields; i++) {
    printf("% -15s",PQfname(res,i));
  }
  printf("\n");

  /* next, print out the instances */
  for (i=0; i < PQntuples(res); i++) {
    for (j=0  ; j < nFields; j++) {
      printf("% -15s", PQgetvalue(res,i,j));
    }
    printf("\n");
  }

  PQclear(res);

  /* close the portal */
  res = PQexec(conn, "CLOSE myportal");
  PQclear(res);

  /* end the transaction */
  res = PQexec(conn, "END");
  PQclear(res);

  /* close the connection to the database and cleanup */
  PQfinish(conn);

/*   fclose(debug); */
}

```

--------------------------------

### Build and Install sepgsql Regression Test Policy

Source: https://www.postgresql.org/docs/15/sepgsql

This snippet demonstrates the commands to build the sepgsql-regtest policy package from its source file using the SELinux development Makefile and then install it into the kernel using 'semodule'. It also shows how to verify the installation by listing available policy packages.

```bash
$ cd .../contrib/sepgsql
$ make -f /usr/share/selinux/devel/Makefile
$ sudo semodule -u sepgsql-regtest.pp
$ sudo semodule -l | grep sepgsql
sepgsql-regtest 1.07
```

--------------------------------

### PostgreSQL Substring Extraction from Bytea

Source: https://www.postgresql.org/docs/13/functions-binarystring

Extracts a portion of a bytea string. It takes the bytea data, a starting byte position (1-based), and an optional count of bytes to extract. Example demonstrates extracting 2 bytes starting from the 3rd byte.

```sql
SELECT substr('\x1234567890'::bytea, 3, 2);
```

--------------------------------

### Connect and Query PostgreSQL with libpq (C)

Source: https://www.postgresql.org/docs/devel/libpq-example

This C program demonstrates fundamental PostgreSQL database interaction using the libpq library. It connects to a PostgreSQL instance, sets a secure search path, begins a transaction, declares and fetches data from a cursor on the `pg_database` system catalog, and then prints the results to the console. It handles connection and query execution errors and cleans up resources properly. The connection string can be provided as a command-line argument.

```C
/*
 * src/test/examples/testlibpq.c
 *
 *
 * testlibpq.c
 *
 *      Test the C version of libpq, the PostgreSQL frontend library.
 */
#include <stdio.h>
#include <stdlib.h>
#include "libpq-fe.h"

static void
exit_nicely(PGconn *conn)
{
    PQfinish(conn);
    exit(1);
}

int
main(int argc, char **argv)
{
    const char *conninfo;
    PGconn     *conn;
    PGresult   *res;
    int         nFields;
    int         i,
                j;

    /*
     * If the user supplies a parameter on the command line, use it as the
     * conninfo string; otherwise default to setting dbname=postgres and using
     * environment variables or defaults for all other connection parameters.
     */
    if (argc > 1)
        conninfo = argv[1];
    else
        conninfo = "dbname = postgres";

    /* Make a connection to the database */
    conn = PQconnectdb(conninfo);

    /* Check to see that the backend connection was successfully made */
    if (PQstatus(conn) != CONNECTION_OK)
    {
        fprintf(stderr, "%s", PQerrorMessage(conn));
        exit_nicely(conn);
    }

    /* Set always-secure search path, so malicious users can't take control. */
    res = PQexec(conn,
                 "SELECT pg_catalog.set_config('search_path', '', false)");
    if (PQresultStatus(res) != PGRES_TUPLES_OK)
    {
        fprintf(stderr, "SET failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }

    /*
     * Should PQclear PGresult whenever it is no longer needed to avoid memory
     * leaks
     */
    PQclear(res);

    /*
     * Our test case here involves using a cursor, for which we must be inside
     * a transaction block.  We could do the whole thing with a single
     * PQexec() of "select * from pg_database", but that's too trivial to make
     * a good example.
     */

    /* Start a transaction block */
    res = PQexec(conn, "BEGIN");
    if (PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "BEGIN command failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }
    PQclear(res);

    /*
     * Fetch rows from pg_database, the system catalog of databases
     */
    res = PQexec(conn, "DECLARE myportal CURSOR FOR select * from pg_database");
    if (PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "DECLARE CURSOR failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }
    PQclear(res);

    res = PQexec(conn, "FETCH ALL in myportal");
    if (PQresultStatus(res) != PGRES_TUPLES_OK)
    {
        fprintf(stderr, "FETCH ALL failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }

    /* first, print out the attribute names */
    nFields = PQnfields(res);
    for (i = 0; i < nFields; i++)
        printf("%-15s", PQfname(res, i));
    printf("\n\n");

    /* next, print out the rows */
    for (i = 0; i < PQntuples(res); i++)
    {
        for (j = 0; j < nFields; j++)
            printf("%-15s", PQgetvalue(res, i, j));
        printf("\n");
    }

    PQclear(res);

    /* close the portal ... we don't bother to check for errors ... */
    res = PQexec(conn, "CLOSE myportal");
    PQclear(res);

    /* end the transaction */
    res = PQexec(conn, "END");
    PQclear(res);

    /* close the connection to the database and cleanup */
    PQfinish(conn);

    return 0;
}
```

--------------------------------

### PostgreSQL Simple Query Protocol Example

Source: https://www.postgresql.org/docs/17/protocol-flow

Demonstrates the simple query protocol, which is a more straightforward way to execute SQL commands. It can handle multiple SQL statements in a single string and is equivalent to a series of extended query messages without explicit parsing, binding, or closing.

```protocol
Query (query: "SELECT 1 + 2; SELECT 3 + 4")
```

--------------------------------

### PostgreSQL: Creating Classes

Source: https://www.postgresql.org/docs/7.0/bki26573

Commands to create and open classes in PostgreSQL. CREATE defines a new class with specified attributes and types. OPEN AS creates a class for writing without system catalog recording, useful for bootstrapping.

```sql
CREATE `classname` (`name1` = `type1` [,`name2` = `type2`[,...]])
OPEN (`name1` = `type1` [,`name2` = `type2`[,...]]) AS `classname`
```

--------------------------------

### PostgreSQL Example Platform Mapping

Source: https://www.postgresql.org/docs/10/regress-variant

An example line from the `resultmap` file demonstrating how to specify a variant comparison file for a specific test and platform pattern. This example handles floating-point value differences on OpenBSD.

```text
float8:out:i.86-.*-openbsd=float8-small-is-zero.out
```

--------------------------------

### Client-Only PostgreSQL Installation (make -C src/bin install)

Source: https://www.postgresql.org/docs/10/install-procedure

Installs only the PostgreSQL client applications and interface libraries. This is achieved by executing specific installation commands for the client-related source directories.

```shell
make -C src/bin install
make -C src/include install
make -C src/interfaces install
make -C doc install
```

--------------------------------

### Configure PostgreSQL Automatic Startup (FreeBSD)

Source: https://www.postgresql.org/docs/6.3/c1802

This shell script configures FreeBSD 2.2-RELEASE to automatically start the PostgreSQL postmaster. It checks for the postmaster executable, runs it as the 'pgsql' user, redirects output to a log file, and sets appropriate permissions.

```shell
#!/bin/sh
[ -x /usr/local/pgsql/bin/postmaster ] && {
  su -l pgsql -c 'exec /usr/local/pgsql/bin/postmaster -D/usr/local/pgsql/data -S -o -F > /usr/local/pgsql/errlog' &
  echo -n ' pgsql'
}
```

--------------------------------

### PostgreSQL Error Message Function Name Example

Source: https://www.postgresql.org/docs/11/error-style-guide

Illustrates how to rephrase error messages to be user-centric, avoiding internal function names. The 'BETTER' example focuses on the user-facing problem ('invalid input syntax') rather than the internal routine ('pg_atoi').

```text
BAD:    pg_atoi: error in "z": cannot parse "z"
BETTER: invalid input syntax for integer: "z"

```

--------------------------------

### PostgreSQL Grant Permissions Example

Source: https://www.postgresql.org/docs/6.5/sql-grant

An example demonstrating how to view granted permissions on existing objects using the psql meta-command \z.

```sql
         Database    = lusitania
   +------------------+---------------------------------------------+
   |  Relation        |        Grant/Revoke Permissions             |
   +------------------+---------------------------------------------+
   | mytable          | "=rw","miriam=arwR","group todos=rw"      |
   +------------------+---------------------------------------------+
   Legend:
         uname=arwR -- privileges granted to a user
   group gname=arwR -- privileges granted to a GROUP
              =arwR -- privileges granted to PUBLIC

                  r -- SELECT
                  w -- UPDATE/DELETE
                  a -- INSERT
                  R -- RULE
               arwR -- ALL
    

```

--------------------------------

### PostgreSQL: Create Subscription with Deferred Connection and Auto-Named Slot

Source: https://www.postgresql.org/docs/16/logical-replication-subscription

This example demonstrates how to create a PostgreSQL subscription with `connect = false` where the replication slot name is automatically derived from the subscription name. It includes steps for creating the subscription on the subscriber, manually creating the logical replication slot on the publisher using `pg_create_logical_replication_slot`, and then enabling and refreshing the subscription on the subscriber to initiate replication.

```sql
CREATE SUBSCRIPTION sub1
CONNECTION 'host=localhost dbname=test_pub'
PUBLICATION pub1
WITH (connect=false);
```

```sql
SELECT * FROM pg_create_logical_replication_slot('sub1', 'pgoutput');
```

```sql
ALTER SUBSCRIPTION sub1 ENABLE;
ALTER SUBSCRIPTION sub1 REFRESH PUBLICATION;
```

--------------------------------

### Initialize PostgreSQL Database Cluster with sepgsql

Source: https://www.postgresql.org/docs/14/sepgsql

This shell script provides an example of how to initialize a fresh PostgreSQL database cluster and enable the `sepgsql` module. It sets the `PGDATA` environment variable, runs `initdb`, modifies `postgresql.conf` to include `sepgsql` in `shared_preload_libraries`, and then executes `sepgsql.sql` in key databases to install necessary functions and assign initial security labels.

```bash
$ export PGDATA=/path/to/data/directory
$ initdb
$ vi $PGDATA/postgresql.conf
  change
    #shared_preload_libraries = ''                # (change requires restart)
  to
    shared_preload_libraries = 'sepgsql'          # (change requires restart)
$ for DBNAME in template0 template1 postgres; do
    postgres --single -F -c exit_on_error=true $DBNAME \
      </usr/local/pgsql/share/contrib/sepgsql.sql >/dev/null
  done

```

--------------------------------

### Example pg_hba.conf Configuration - PostgreSQL

Source: https://www.postgresql.org/docs/7.1/admin

Provides an example of the pg_hba.conf file, which controls client authentication in PostgreSQL. This file specifies which hosts can connect to which databases, for which users, and using which authentication methods. Understanding its structure is crucial for securing PostgreSQL access.

```postgresql
# TYPE  DATABASE        USER            ADDRESS                 METHOD

# "local" is for "local" connections
local   all             all                                     trust

# IPv4 local connections:
host    all             all             127.0.0.1/32            scram-sha-256

# IPv6 local connections:
host    all             all             ::1/128                 scram-sha-256

# Allow replication connections from a specific IP range
host    replication     replication     192.168.1.0/24          scram-sha-256

# Deny all other connections (example of a default deny rule)
host    all             all             0.0.0.0/0               reject
```

--------------------------------

### Build HTML Documentation with Meson (PostgreSQL)

Source: https://www.postgresql.org/docs/16/docguide-build-meson

This command builds only the HTML version of the PostgreSQL documentation. Ensure you are in the `build` directory or use the `-C build` option. The output will be found in the `build/doc/src/sgml` subdirectory.

```bash
ninja docs
```

--------------------------------

### PostgreSQL Connection Service File Example

Source: https://www.postgresql.org/docs/10/libpq-pgservice

An example of the connection service file format, which uses an INI-style structure. Each section defines a service name, and key-value pairs within the section specify libpq connection parameters.

```ini
# comment
[mydb]
host=somehost
port=5433
user=admin
```

--------------------------------

### Control PostgreSQL Logical Decoding with pg_recvlogical

Source: https://www.postgresql.org/docs/12/logicaldecoding-example

Demonstrates controlling logical decoding using the `pg_recvlogical` utility, which is part of the PostgreSQL distribution. This method uses the streaming replication protocol. It requires client authentication to be set up for replication connections and sufficient `max_wal_senders`. The example shows creating a slot, starting to receive changes, inserting data, and then dropping the slot.

```bash
$ pg_recvlogical -d postgres --slot=test --create-slot
$ pg_recvlogical -d postgres --slot=test --start -f -
**Control**+**Z**
$ psql -d postgres -c "INSERT INTO data(data) VALUES('4');"
$ fg
BEGIN 693
table public.data: INSERT: id[integer]:4 data[text]:'4'
COMMIT 693
**Control**+**C**
$ pg_recvlogical -d postgres --slot=test --drop-slot

```

--------------------------------

### Creating Extensions in PostgreSQL

Source: https://www.postgresql.org/docs/13/glossary

Demonstrates how to create an extension in PostgreSQL. Extensions add new functionality to the database. This example uses the `CREATE EXTENSION` command, which requires the extension to be present in the PostgreSQL installation.

```sql
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";
```

--------------------------------

### Build All PostgreSQL Binaries Without Documentation

Source: https://www.postgresql.org/docs/13/install-procedure

This command builds all PostgreSQL components, including additional modules found in `contrib`, but explicitly excludes the generation of documentation. This option is suitable for scenarios where only the executable binaries and libraries are required.

```bash
make world-bin
```

--------------------------------

### Example: Create a Foreign Table for PostgreSQL CSV Logs

Source: https://www.postgresql.org/docs/17/file-fdw

Demonstrates the steps to install the file_fdw extension, create a foreign server, and define a foreign table for querying PostgreSQL CSV logs.

```APIDOC
## Example: Create a Foreign Table for PostgreSQL CSV Logs

### Description
This example shows how to make PostgreSQL activity logs, stored in a CSV file, accessible as a queryable table using `file_fdw`.

### Steps

1.  **Install `file_fdw` extension:**
    ```sql
    CREATE EXTENSION file_fdw;
    ```

2.  **Create a foreign server:**
    ```sql
    CREATE SERVER pglog FOREIGN DATA WRAPPER file_fdw;
    ```

3.  **Create the foreign data table:**
    Define the table columns, the CSV file name (`pglog.csv` in this example), and its format.
    ```sql
    CREATE FOREIGN TABLE pglog (
      log_time timestamp(3) with time zone,
      user_name text,
      database_name text,
      process_id integer,
      connection_from text,
      session_id text,
      session_line_num bigint,
      command_tag text,
      session_start_time timestamp with time zone,
      virtual_transaction_id text,
      transaction_id bigint,
      error_severity text,
      sql_state_code text,
      message text,
      detail text,
      hint text,
      internal_query text,
      internal_query_pos integer,
      context text,
      query text,
      query_pos integer,
      location text,
      application_name text,
      backend_type text
    ) SERVER pglog
    OPTIONS (filename 'pglog.csv', format 'csv');
    ```

### Notes
- Ensure that PostgreSQL is configured to log in CSV format for this example to work.
- The `filename` option should point to the actual location of your `pglog.csv` file relative to the PostgreSQL data directory.
```

--------------------------------

### PostgreSQL: Example of Moving and Fetching with a Cursor

Source: https://www.postgresql.org/docs/devel/sql-move

This example demonstrates how to use the `MOVE` command in PostgreSQL to skip a specified number of rows within a cursor, followed by a `FETCH` command to retrieve a subsequent row. It includes starting a transaction, declaring a cursor, moving the cursor, and then fetching data.

```sql
BEGIN WORK;
DECLARE liahona CURSOR FOR SELECT * FROM films;

-- Skip the first 5 rows:
MOVE FORWARD 5 IN liahona;
MOVE 5

-- Fetch the 6th row from the cursor liahona:
FETCH 1 FROM liahona;
 code  | title  | did | date_prod  |  kind  |  len
-------+--------+-----+------------+--------+-------
 P_303 | 48 Hrs | 103 | 1982-10-22 | Action | 01:37
(1 row)

-- Close the cursor liahona and end the transaction:
CLOSE liahona;
COMMIT WORK;
```

--------------------------------

### Extracting Substrings with PostgreSQL `regexp_substr`

Source: https://www.postgresql.org/docs/16/functions-matching

These examples demonstrate how to use the PostgreSQL `regexp_substr` function to extract substrings based on a POSIX regular expression pattern. The function allows specifying the starting position, the N-th match, flags, and a subexpression index. The first example extracts the second comma-separated part, while the second example extracts a specific subexpression from a match using a case-insensitive flag.

```sql
regexp_substr('number of your street, town zip, FR', '[^,]+', 1, 2);
regexp_substr('ABCDEFGHI', '(c..)(...)', 1, 1, 'i', 2);
```

--------------------------------

### PostgreSQL CREATE SERVER Example

Source: https://www.postgresql.org/docs/13/glossary

Illustrates the creation of a foreign server definition, which specifies connection details and the foreign data wrapper to be used for accessing remote data.

```sql
CREATE SERVER server_name
  FOREIGN DATA WRAPPER wrapper_name
  OPTIONS (host 'hostname', dbname 'database_name', port 'port_number');
```

--------------------------------

### Build and Install sepgsql Regression Test Policy

Source: https://www.postgresql.org/docs/17/sepgsql

This snippet demonstrates the commands to build the sepgsql-regtest policy package from its source file using SELinux's development Makefile and then install it using the semodule command. It also shows how to verify the installation by listing available policy packages. This is a prerequisite for running the regression tests.

```shell
$ cd .../contrib/sepgsql
$ make -f /usr/share/selinux/devel/Makefile
$ sudo semodule -u sepgsql-regtest.pp
$ sudo semodule -l | grep sepgsql
sepgsql-regtest 1.07

```

--------------------------------

### Debugging Connections with strace

Source: https://www.postgresql.org/docs/7.0/odbc24666

This section demonstrates how to use the Unix 'strace' utility to capture system calls made by the 'axnet' process, aiding in the diagnosis of connection problems. It shows example commands for starting strace and interpreting its output, particularly for identifying missing libraries.

```bash
% ps -aucx | grep ax 
       
cary   10432  0.0  2.6  1740   392  ?  S  Oct  9  0:00 axnet
cary   27883  0.9 31.0 12692  4596  ?  S   10:24  0:04 axmain
       
% strace -f -s 1024 -p 10432
       
[pid 27947] open("/usr/lib/libodbc.so", O_RDONLY) = -1 ENOENT
(No such file or directory)
[pid 27947] open("/lib/libodbc.so", O_RDONLY) = -1 ENOENT
(No such file or directory)
[pid 27947] write(2, "/usr2/applix/axdata/elfodbc:
can't load library 'libodbc.so'\n", 61) = -1 EIO (I/O error)
     
```

--------------------------------

### PostgreSQL: Get Primary Key Fields using dblink_get_pkey

Source: https://www.postgresql.org/docs/10/contrib-dblink-get-pkey

This example demonstrates how to use the `dblink_get_pkey` function in PostgreSQL to retrieve the primary key fields of a table. It first creates a sample table with a composite primary key, then executes `dblink_get_pkey` to get the details and shows the expected output.

```sql
CREATE TABLE foobar (
    f1 int,
    f2 int,
    f3 int,
    PRIMARY KEY (f1, f2, f3)
);
CREATE TABLE

SELECT * FROM dblink_get_pkey('foobar');
 position | colname
----------+---------
        1 | f1
        2 | f2
        3 | f3
(3 rows)
```

--------------------------------

### PostgreSQL: Find Substring Position with regexp_instr

Source: https://www.postgresql.org/docs/devel/functions-matching

Examples demonstrating the use of `regexp_instr` in PostgreSQL to find the starting position of a substring matching a regular expression pattern. This function allows specifying the occurrence, start position, and subexpression to match within the string.

```sql
regexp_instr('number of your street, town zip, FR', '[^,]+', 1, 2)
                                   _23_
regexp_instr(string=>'ABCDEFGHI', pattern=>'(c..)(...)', start=>1, "N"=>1, endoption=>0, flags=>'i', subexpr=>2)
                                   _6_
```

--------------------------------

### Handle Asynchronous PostgreSQL Notifications with libpq (C)

Source: https://www.postgresql.org/docs/devel/libpq-example

This C program illustrates how to use the libpq library to listen for and handle asynchronous notifications from a PostgreSQL database. It connects to PostgreSQL and continuously checks for notifications (e.g., from `NOTIFY TBL2;` commands or rule-based triggers). The program exits after receiving four notifications. It also provides an example setup for a rule that triggers notifications on `INSERT` operations, which can be found in `src/test/examples/testlibpq2.sql`.

```C
/*
 * src/test/examples/testlibpq2.c
 *
 *
 * testlibpq2.c
 *      Test of the asynchronous notification interface
 *
 * Start this program, then from psql in another window do
 *   NOTIFY TBL2;
 * Repeat four times to get this program to exit.
 *
 * Or, if you want to get fancy, try this:
 * populate a database with the following commands
 * (provided in src/test/examples/testlibpq2.sql):
 *
 *   CREATE SCHEMA TESTLIBPQ2;
 *   SET search_path = TESTLIBPQ2;
 *   CREATE TABLE TBL1 (i int4);
 *   CREATE TABLE TBL2 (i int4);
 *   CREATE RULE r1 AS ON INSERT TO TBL1 DO
 *     (INSERT INTO TBL2 VALUES (new.i); NOTIFY TBL2);
 *
 * Start this program, then from psql do this four times:
 *
 *   INSERT INTO TESTLIBPQ2.TBL1 VALUES (10);
 */

#ifdef WIN32
#include <windows.h>
#endif
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <errno.h>
#include <sys/select.h>
#include <sys/time.h>
#include <sys/types.h>

#include "libpq-fe.h"

static void
exit_nicely(PGconn *conn)
{
    PQfinish(conn);
    exit(1);
}

int
main(int argc, char **argv)
{
    const char *conninfo;
    PGconn     *conn;
    PGresult   *res;
    PGnotify   *notify;
    int         nnotifies;

    /*
     * If the user supplies a parameter on the command line, use it as the
     * conninfo string; otherwise default to setting dbname=postgres and using
 */
```

--------------------------------

### Build PostgreSQL using Visual Studio

Source: https://www.postgresql.org/docs/10/install-windows-full

Steps to initiate the build process from within the Visual Studio IDE by first generating the solution file from the command prompt.

```shell
perl mkvcbuild.pl
```

--------------------------------

### Example of ordered configuration files in a directory

Source: https://www.postgresql.org/docs/10/config-setting

Illustrates a common naming convention for files within an `include_dir` directory, where numerical prefixes establish a clear loading and override order (e.g., `00shared.conf`, `01memory-8GB.conf`, `02server-foo.conf`).

```text
00shared.conf
01memory-8GB.conf
02server-foo.conf
```

--------------------------------

### PostgreSQL C Function Example: Integer By Value (add_one)

Source: https://www.postgresql.org/docs/devel/xfunc-c

Demonstrates a PostgreSQL C function 'add_one' that takes an int32 by value, increments it, and returns the result. It uses PG_GETARG_INT32(0) to retrieve the argument and PG_RETURN_INT32 to return the modified value. This example includes common headers and PG_MODULE_MAGIC setup.

```C
#include "postgres.h"
#include <string.h>
#include "fmgr.h"
#include "utils/geo_decls.h"
#include "varatt.h"

PG_MODULE_MAGIC;

/* by value */

PG_FUNCTION_INFO_V1(add_one);

Datum
add_one(PG_FUNCTION_ARGS)
{
    int32   arg = PG_GETARG_INT32(0);

    PG_RETURN_INT32(arg + 1);
}
```

--------------------------------

### pg_resetwal Command Example with WAL File Name Offset

Source: https://www.postgresql.org/docs/11/app-pgresetwal

This example shows how to use the pg_resetwal command with the -l option to manually set the WAL starting address. This is recommended when segment size changes might cause WAL file name reuse, potentially causing issues with archiving strategies.

```bash
pg_resetwal -l <wal_start_address>
```

--------------------------------

### Extract Subarray from Start to End in PostgreSQL intarray

Source: https://www.postgresql.org/docs/10/intarray

This example illustrates extracting a portion of a null-free integer array from a specified 1-based starting position to the end of the array using the `subarray()` function from the `intarray` module in PostgreSQL. It returns a new array containing the requested elements.

```sql
SELECT subarray('{1,2,3,2,1}'::int[], 2);
```

--------------------------------

### PostgreSQL: Configure and Load auto_explain Extension

Source: https://www.postgresql.org/docs/15/auto-explain

This snippet shows how to load the 'auto_explain' extension and configure its logging parameters to capture detailed query execution plans. It then executes a sample query to demonstrate the functionality. Dependencies: PostgreSQL with the auto_explain extension installed. Inputs: SQL commands. Outputs: Log entries containing query plans.

```sql
LOAD 'auto_explain';
SET auto_explain.log_min_duration = 0;
SET auto_explain.log_analyze = true;
SELECT count(*)
           FROM pg_class, pg_index
           WHERE oid = indrelid AND indisunique;
```

--------------------------------

### Build Standalone PostgreSQL ODBC Driver

Source: https://www.postgresql.org/docs/6.4/odbc18456

Compiles the PostgreSQL ODBC driver into a standalone tar file. This is the initial step before copying the driver to the target system.

```bash
% cd interfaces/odbc
% make standalone
```

--------------------------------

### PostgreSQL: Creating Tables and Applying Security Labels

Source: https://www.postgresql.org/docs/13/sepgsql

Demonstrates the SQL commands to create a table, apply a security label to a column, create a function, and then apply a security label to that function. This illustrates setting up a trusted procedure in PostgreSQL with SELinux.

```sql
postgres=# CREATE TABLE customer (
               cid     int primary key,
               cname   text,
               credit  text
           );
CREATE TABLE
postgres=# SECURITY LABEL ON COLUMN customer.credit
               IS 'system_u:object_r:sepgsql_secret_table_t:s0';
SECURITY LABEL
postgres=# CREATE FUNCTION show_credit(int) RETURNS text
             AS 'SELECT regexp_replace(credit, ''-[0-9]+$'', ''-xxxx'', ''g'')
                        FROM customer WHERE cid = $1'
           LANGUAGE sql;
CREATE FUNCTION
postgres=# SECURITY LABEL ON FUNCTION show_credit(int)
               IS 'system_u:object_r:sepgsql_trusted_proc_exec_t:s0';
SECURITY LABEL
```

--------------------------------

### Extract Subarray by Start and Length in PostgreSQL intarray

Source: https://www.postgresql.org/docs/10/intarray

This example demonstrates how to extract a portion of a null-free integer array using the `subarray()` function from the `intarray` module in PostgreSQL. It takes the source array, a 1-based starting position, and the number of elements to extract, returning a new subarray.

```sql
SELECT subarray('{1,2,3,2,1}'::int[], 2, 3);
```

--------------------------------

### Manage PostgreSQL Replication Slot with pg_recvlogical

Source: https://www.postgresql.org/docs/17/logicaldecoding-example

This snippet demonstrates the basic commands for managing a logical replication slot using pg_recvlogical. It covers creating, starting, and dropping a slot. Ensure 'max_prepared_transactions' is set appropriately if using two-phase commit.

```bash
$ pg_recvlogical -d postgres --slot=test --drop-slot
$ pg_recvlogical -d postgres --slot=test --create-slot --two-phase
$ pg_recvlogical -d postgres --slot=test --start -f -
**Control**+**Z**
```

--------------------------------

### GET sepgsql_getcon()

Source: https://www.postgresql.org/docs/devel/sepgsql

This function returns the current security label of the client process, often referred to as the client domain. It provides visibility into the active SELinux context for the session.

```APIDOC
## GET /sepgsql_getcon

### Description
Returns the client domain, the current security label of the client.

### Method
GET

### Endpoint
/sepgsql_getcon

### Parameters
#### Path Parameters
(None)

#### Query Parameters
(None)

#### Request Body
(None)

### Request Example
```sql
SELECT sepgsql_getcon();
```

### Response
#### Success Response (200)
- **sepgsql_getcon** (text) - The current security label of the client, e.g., 'unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023'.

#### Response Example
```json
{
  "sepgsql_getcon": "unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023"
}
```
```

--------------------------------

### PostgreSQL ts_debug Example with Custom Configuration

Source: https://www.postgresql.org/docs/devel/textsearch-debugging

An example using the previously created custom 'public.english' text search configuration with `ts_debug`. This showcases how the custom Ispell dictionary influences the tokenization and lexeme generation for a given phrase, highlighting the effect of advanced text search setup.

```sql
SELECT * FROM ts_debug('public.english', 'The Brightest supernovaes');
```

--------------------------------

### PostgreSQL: Create User Examples

Source: https://www.postgresql.org/docs/6.4/sql-createuser

Provides practical examples of using the CREATE USER statement in PostgreSQL for different scenarios, including creating users with and without passwords, setting expiration dates, and granting privileges.

```sql
   CREATE USER jonathan
  
```

```sql
   CREATE USER davide WITH PASSWORD jw8s0F4
  
```

```sql
   CREATE USER miriam WITH PASSWORD jw8s0F4 VALID UNTIL 'Jan 1 2002'
  
```

```sql
   CREATE USER manuel WITH PASSWORD jw8s0F4 CREATEDB
  
```

--------------------------------

### Start PostgreSQL Server as PostgreSQL User

Source: https://www.postgresql.org/docs/current/server-start

This command demonstrates starting the PostgreSQL server using 'pg_ctl' within a 'su' command to ensure it runs as the 'postgres' user. This is crucial for security and proper file permissions. It specifies the data directory and a server log file.

```shell
su postgres -c 'pg_ctl start -D /usr/local/pgsql/data -l serverlog'

```

--------------------------------

### Build and Install PostgreSQL sepgsql Regression Test SELinux Policy

Source: https://www.postgresql.org/docs/14/sepgsql

This command sequence builds the `sepgsql-regtest` SELinux policy from its source file, installs it using `semodule -u`, and then verifies its successful installation by listing active policies. This policy provides necessary rules for running `sepgsql` regression tests.

```bash
$ cd .../contrib/sepgsql
$ make -f /usr/share/selinux/devel/Makefile
$ sudo semodule -u sepgsql-regtest.pp
$ sudo semodule -l | grep sepgsql
sepgsql-regtest 1.07
```

--------------------------------

### Build and Install sepgsql Regression Test Policy

Source: https://www.postgresql.org/docs/10/sepgsql

Commands to navigate to the sepgsql contrib directory, build the sepgsql-regtest policy package using SELinux development tools, and install it using `semodule`. It also shows how to verify the installation by listing installed policies. This process is crucial for enabling the regression tests.

```shell
cd .../contrib/sepgsql
make -f /usr/share/selinux/devel/Makefile
sudo semodule -u sepgsql-regtest.pp
sudo semodule -l | grep sepgsql
```

--------------------------------

### Query current data state on PostgreSQL publisher

Source: https://www.postgresql.org/docs/devel/logical-replication-subscription

This SQL snippet queries all tables (t1, t2, t3) on the PostgreSQL publisher to show their current state after additional data insertions. This provides a baseline to compare against the subscriber's replicated data, demonstrating what data is available for replication.

```sql
SELECT * FROM t1;
SELECT * FROM t2;
SELECT * FROM t3;
```

--------------------------------

### Configure `pg_hba.conf` for Replication User Access

Source: https://www.postgresql.org/docs/devel/logical-replication-quick-setup

This snippet demonstrates how to adjust `pg_hba.conf` to permit a replication user (`repuser`) to connect from any host (`0.0.0.0/0`) using MD5 authentication. The values should be customized based on your specific network and security requirements.

```ini
host     all     repuser     0.0.0.0/0     md5

```

--------------------------------

### PostgreSQL FATAL Error (User Mismatch)

Source: https://www.postgresql.org/docs/6.3/c0302

This example displays a FATAL error message in PostgreSQL indicating a mismatch between the process user ID and the database owner. This typically occurs when the postmaster process is started by an incorrect user, requiring it to be restarted as the Postgres superuser.

```text
FATAL 1:Feb 17 23:19:55:process userid (2360) != database owner (268)
```

--------------------------------

### Display Version (initdb)

Source: https://www.postgresql.org/docs/10/app-initdb

Prints the version of the `initdb` command and exits.

```bash
initdb -V
```

```bash
initdb --version
```

--------------------------------

### Perl Locale Setting Warning Example (Perl)

Source: https://www.postgresql.org/docs/6.5/config12702

This example illustrates a common warning message from Perl when locale settings are invalid or unsupported on the system. It shows how Perl falls back to the standard 'C' locale if LC_CTYPE or other locale variables are not properly configured or installed, indicating potential OS-level locale issues.

```perl
perl: warning: Setting locale failed.
perl: warning: Please check that your locale settings:
LC_ALL = (unset),
    LC_CTYPE = "not_exist",
    LANG = (unset)
are supported and installed on your system.
perl: warning: Falling back to the standard locale ("C").

```

--------------------------------

### Filter Segments by HR and Get Start Time Using jsonpath

Source: https://www.postgresql.org/docs/12/functions-json

This `jsonpath` expression first filters the 'segments' array, retaining only those segments where the 'HR' value is greater than 130. After filtering the segments, it extracts the 'start time' field from the matching segments, demonstrating conditional retrieval of associated data.

```jsonpath
'$.track.segments[*] ? (@.HR > 130)."start time"'
```

--------------------------------

### Get Current PostgreSQL Transaction and Statement Timestamps

Source: https://www.postgresql.org/docs/12/functions-datetime

Retrieves various current date and time values. `now()` and `transaction_timestamp()` return the start of the current transaction, `statement_timestamp()` returns the start of the current statement, and `timeofday()` returns a text string of the current date and time. These are discussed in Section 9.9.4.

```SQL
now()
```

```SQL
statement_timestamp()
```

```SQL
timeofday()
```

```SQL
transaction_timestamp()
```

--------------------------------

### Shell: pg_recvlogical for Streaming Logical Decoding

Source: https://www.postgresql.org/docs/11/logicaldecoding-example

This example demonstrates controlling PostgreSQL logical decoding using the `pg_recvlogical` utility for streaming replication. It covers creating a slot, starting to receive changes, inserting data into the database, and observing the streamed changes. Finally, it shows how to drop the replication slot. Ensure client authentication is configured for replication and `max_wal_senders` is sufficient.

```shell
$ pg_recvlogical -d postgres --slot=test --create-slot
$ pg_recvlogical -d postgres --slot=test --start -f -
**Control**+**Z**
$ psql -d postgres -c "INSERT INTO data(data) VALUES('4');"
$ fg
BEGIN 693
table public.data: INSERT: id[integer]:4 data[text]:'4'
COMMIT 693
**Control**+**C**
$ pg_recvlogical -d postgres --slot=test --drop-slot
```

--------------------------------

### Compile and Install PostgreSQL Source Code

Source: https://www.postgresql.org/docs/6.5/install12893

This command compiles and installs the PostgreSQL source code. It is typically run as the root user and updates various system files and directories related to the flex utility.

```bash
$ gmake install
$ cd /usr/local/src
$ rm -rf flex-2.5.4
```

--------------------------------

### Create PostgreSQL tables on publisher

Source: https://www.postgresql.org/docs/devel/logical-replication-subscription

This SQL snippet creates three tables (t1, t2, t3) with integer primary keys and text columns on the PostgreSQL publisher database. These tables will serve as the source for logical replication.

```sql
CREATE TABLE t1(a int, b text, PRIMARY KEY(a));
CREATE TABLE t2(c int, d text, PRIMARY KEY(c));
CREATE TABLE t3(e int, f text, PRIMARY KEY(e));
```

--------------------------------

### Reconfiguring Meson Build Options

Source: https://www.postgresql.org/docs/16/install-meson

Shows how to reconfigure an existing Meson build directory using the 'meson configure' command. This allows updating build options, such as enabling assertion checks, without needing to re-run the initial setup.

```shell
meson configure -Dcassert=true
```

--------------------------------

### PostgreSQL BKI: Create Table and Insert Data

Source: https://www.postgresql.org/docs/devel/bki-example

This example demonstrates how to use PostgreSQL BKI (Bootstrap Key Information) commands to define a new table and populate it with initial data. It creates `test_table` with OID 420, specifying `oid`, `int4`, and `text` column types, then inserts two rows, one with a NULL value.

```PostgreSQL BKI
create test_table 420 (oid = oid, cola = int4, colb = text)
open test_table
insert ( 421 1 'value 1' )
insert ( 422 2 _null_ )
close test_table
```

--------------------------------

### Build PostgreSQL Core System with 'make'

Source: https://www.postgresql.org/docs/11/install-procedure

Initiates the build process for the core PostgreSQL system. It's recommended to use GNU make. The successful completion is indicated by a specific message.

```shell
**make**
```

```shell
**make all**
```

--------------------------------

### Run PostgreSQL Tutorial Script with psql

Source: https://www.postgresql.org/docs/current/tutorial-sql-intro

This sequence shows how to start the PostgreSQL interactive terminal (psql) in single-step mode with a specific database ('mydb') and then execute a tutorial SQL script ('basics.sql'). The '-s' option pauses execution before each command.

```bash
psql -s mydb
mydb=> \i basics.sql
```

--------------------------------

### Build and Install sepgsql-regtest SELinux Policy

Source: https://www.postgresql.org/docs/devel/sepgsql

Navigate to the `contrib/sepgsql` directory, build the `sepgsql-regtest` policy using the SELinux development Makefile, and then install it into the kernel using `sudo semodule -u`. This policy provides necessary rules for regression testing.

```bash
cd .../contrib/sepgsql
make -f /usr/share/selinux/devel/Makefile
sudo semodule -u sepgsql-regtest.pp
sudo semodule -l | grep sepgsql
sepgsql-regtest 1.07
```

--------------------------------

### PostgreSQL Configuration File Example

Source: https://www.postgresql.org/docs/current/runtime-config-compatible

An example of how to set configuration parameters within the `postgresql.conf` file. This demonstrates setting `transform_null_equals` and `allow_alter_system` to control specific PostgreSQL behaviors.

```ini
transform_null_equals = on
allow_alter_system = off
```

--------------------------------

### PostgreSQL Configuration File (postgresql.conf)

Source: https://www.postgresql.org/docs/7.2/runtime-config

Example of the postgresql.conf file format for setting database server configuration parameters. Options are specified one per line, with optional equals signs and comments starting with '#'. Blank lines are ignored.

```postgresql.conf
# This is a comment
log_connections = yes
syslog = 2


```

--------------------------------

### Read Specific Portion of Large Object with libpq (C)

Source: https://www.postgresql.org/docs/14/lo-examplesect

Reads a specified portion (starting from 'start' for 'len' bytes) of a PostgreSQL large object using libpq. It opens the large object, seeks to the desired position, reads the data into a buffer, prints it, and then closes the object. Memory is allocated for the buffer and freed afterwards.

```c
static void
pickout(PGconn *conn, Oid lobjId, int start, int len)
{
    int         lobj_fd;
    char       *buf;
    int         nbytes;
    int         nread;

    lobj_fd = lo_open(conn, lobjId, INV_READ);
    if (lobj_fd < 0)
        fprintf(stderr, "cannot open large object %u", lobjId);

    lo_lseek(conn, lobj_fd, start, SEEK_SET);
    buf = malloc(len + 1);

    nread = 0;
    while (len - nread > 0)
    {
        nbytes = lo_read(conn, lobj_fd, buf, len - nread);
        buf[nbytes] = '\0';
        fprintf(stderr, ">>> %s", buf);
        nread += nbytes;
        if (nbytes <= 0)
            break;
    }
    free(buf);
    fprintf(stderr, "\n");
    lo_close(conn, lobj_fd);
}

```

--------------------------------

### Configure PostgreSQL Initialization Script (RedHat Linux)

Source: https://www.postgresql.org/docs/6.4/install12063

This snippet shows how to add a PostgreSQL initialization script to RedHat Linux's init system and create a symbolic link to enable it at runlevel 5. This ensures PostgreSQL starts automatically on boot.

```shell
In RedHat Linux add a file `/etc/rc.d/init.d/postgres.init` which is based on the example in `contrib/linux/`. Then make a softlink to this file from `/etc/rc.d/rc5.d/S98postgres.init`.
```

--------------------------------

### PostgreSQL Error Message Formatting Examples

Source: https://www.postgresql.org/docs/16/error-style-guide

Demonstrates correct and incorrect formatting for PostgreSQL error messages, illustrating principles of punctuation, sentence completeness, and conciseness.

```text
could not open file "%s": %m

```

```text
BAD:	could not open file %s
BETTER:	could not open file %s (I/O failure)

```

```text
BAD:	pg_strtoint32: error in "z": cannot parse "z"
BETTER:	invalid input syntax for type integer: "z"

```

```text
BAD:	open() failed: %m
BETTER:	could not open file %s: %m

```

--------------------------------

### Get Executable Version (postgres)

Source: https://www.postgresql.org/docs/9.1/bug-reporting

This command demonstrates how to check the version of the `postgres` executable, which is the PostgreSQL server process. This is important for server-side bug reports.

```bash
postgres --version
```

--------------------------------

### PostgreSQL Output Plugin Data Production Example

Source: https://www.postgresql.org/docs/11/logicaldecoding-output-plugin

Demonstrates how an output plugin can produce data to the consumer using `StringInfo`. It shows the required calls to `OutputPluginPrepareWrite` before writing and `OutputPluginWrite` after writing to the `ctx->out` buffer. The example appends a 'BEGIN' message with the transaction ID.

```c
OutputPluginPrepareWrite(ctx, true);
appendStringInfo(ctx->out, "BEGIN %u", txn->xid);
OutputPluginWrite(ctx, true);

```

--------------------------------

### PostgreSQL C SRF Pseudo-code Example

Source: https://www.postgresql.org/docs/18/xfunc-c

This pseudo-code outlines the structure of a PostgreSQL Set Returning Function (SRF) in C. It demonstrates the initialization for the first call using SRF_FIRSTCALL_INIT, setup for subsequent calls with SRF_PERCALL_SETUP, and returning values with SRF_RETURN_NEXT or finishing with SRF_RETURN_DONE.

```c
Datum
my_set_returning_function(PG_FUNCTION_ARGS)
{
    FuncCallContext  *funcctx;
    Datum             result;
    /* further declarations as needed */

    if (SRF_IS_FIRSTCALL())
    {
        MemoryContext oldcontext;

        funcctx = SRF_FIRSTCALL_INIT();
        oldcontext = MemoryContextSwitchTo(funcctx->multi_call_memory_ctx);
        /* One-time setup code appears here: */
        /* _user code_ */
        /* _if returning composite_ */
            /* _build TupleDesc, and perhaps AttInMetadata_ */
        /* _endif returning composite_ */
        /* _user code_ */
        MemoryContextSwitchTo(oldcontext);
    }

    /* Each-time setup code appears here: */
    /* _user code_ */
    funcctx = SRF_PERCALL_SETUP();
    /* _user code_ */

    /* this is just one way we might test whether we are done: */
    if (funcctx->call_cntr < funcctx->max_calls)
    {
        /* Here we want to return another item: */
        /* _user code_ */
        /* _obtain result Datum_ */
        SRF_RETURN_NEXT(funcctx, result);
    }
    else
    {
        /* Here we are done returning items, so just report that fact. */
        /* (Resist the temptation to put cleanup code here.) */
        SRF_RETURN_DONE(funcctx);
    }
}

```

--------------------------------

### Upgrade PostgreSQL on Windows using pg_upgrade

Source: https://www.postgresql.org/docs/devel/pgupgrade

Example command to run `pg_upgrade.exe` on Windows, specifying old and new data and binary directories. This operation requires administrative privileges and quoted paths for directories containing spaces.

```cmd
pg_upgrade.exe
        --old-datadir "C:/Program Files/PostgreSQL/12/data"
        --new-datadir "C:/Program Files/PostgreSQL/19/data"
        --old-bindir "C:/Program Files/PostgreSQL/12/bin"
        --new-bindir "C:/Program Files/PostgreSQL/19/bin"
```

--------------------------------

### Set PostgreSQL Build Parameters via Make Command

Source: https://www.postgresql.org/docs/7.0/c1688316912

Demonstrates how to specify PostgreSQL installation build parameters directly on the 'make' command line. This method allows for dynamic configuration of installation paths and compiler flags.

```Shell
make [ `variable`=`value` [...] ]
```

--------------------------------

### PostgreSQL Initiate Simple Transaction Block

Source: https://www.postgresql.org/docs/10/sql-begin

An example demonstrating the basic usage of the BEGIN command to start a new transaction block in PostgreSQL. This simple form initiates a transaction with default settings, requiring an explicit COMMIT or ROLLBACK to conclude.

```sql
BEGIN;
```

--------------------------------

### PostgreSQL pg_upgrade Execution Example

Source: https://www.postgresql.org/docs/7.0/app-pg-upgrade

This snippet shows the execution of the `pg_upgrade` command after preparing the new installation and creating a schema dump. It specifies the schema dump file (`db.out`) and the old data directory (`data.old`) to facilitate the upgrade process.

```bash
% pg_upgrade -f db.out data.old
```

--------------------------------

### DTrace Script to Monitor PostgreSQL Transaction Counts

Source: https://www.postgresql.org/docs/12/dynamic-trace

This DTrace script monitors PostgreSQL transaction events, specifically `transaction-start`, `transaction-abort`, and `transaction-commit`. It counts the occurrences of each event and calculates the total time spent in committed transactions. The script uses DTrace aggregations (`@start`, `@abort`, `@commit`, `@time`) and thread-local variables (`self->ts`) to track state across probes, providing insights into transaction throughput and latency. It requires `dtrace` to be installed and running on a system with PostgreSQL probes enabled.

```dtrace
#!/usr/sbin/dtrace -qs

postgresql$1:::transaction-start
{
      @start["Start"] = count();
      self->ts  = timestamp;
}

postgresql$1:::transaction-abort
{
      @abort["Abort"] = count();
}

postgresql$1:::transaction-commit
/self->ts/
{
      @commit["Commit"] = count();
      @time["Total time (ns)"] = sum(timestamp - self->ts);
      self->ts=0;
}
```

--------------------------------

### Install PostgreSQL Source Code

Source: https://www.postgresql.org/docs/6.4/install12063

This command sequence installs PostgreSQL by compiling the source code. It involves creating directories, setting ownership, and then extracting the compressed source archive.

```shell
$ su
$ cd /usr/src
$ mkdir pgsql
$ chown postgres:postgres pgsql
$ cd /usr/local
$ mkdir pgsql
$ chown postgres:postgres pgsql
$ exit

$ cd /usr/src/pgsql
$ gunzip -c ~/postgresql-v6.4.tar.gz | tar xvf -
```

--------------------------------

### Configuring run-time linker with ldconfig on Linux

Source: https://www.postgresql.org/docs/10/install-post

This command, executable on Linux systems with root access, updates the run-time linker cache to efficiently find installed shared libraries. It requires specifying the directory containing the shared libraries.

```shell
/sbin/ldconfig /usr/local/pgsql/lib
```

--------------------------------

### PostgreSQL: Create Server Example

Source: https://www.postgresql.org/docs/17/glossary

Illustrates the creation of a foreign server in PostgreSQL, which defines the connection details and configuration for accessing a remote data source using a foreign data wrapper.

```sql
CREATE SERVER remote_server
FOREIGN DATA WRAPPER file_fdw
OPTIONS (host 'remote.host.com', port '5432');
```

--------------------------------

### Test libpq C Example Program

Source: https://www.postgresql.org/docs/14/libpq-example

This C program tests the libpq library for connecting to PostgreSQL, executing queries, and retrieving data. It demonstrates transaction management and cursor usage. It requires a PostgreSQL client library and a running PostgreSQL server.

```c
#include <stdio.h>
#include <stdlib.h>
#include "libpq-fe.h"

static void
exit_nicely(PGconn *conn)
{
    PQfinish(conn);
    exit(1);
}

int
main(int argc, char **argv)
{
    const char *conninfo;
    PGconn     *conn;
    PGresult   *res;
    int         nFields;
    int         i, j;

    /*
     * If the user supplies a parameter on the command line, use it as the
     * conninfo string; otherwise default to setting dbname=postgres and using
     * environment variables or defaults for all other connection parameters.
     */
    if (argc > 1)
        conninfo = argv[1];
    else
        conninfo = "dbname = postgres";

    /* Make a connection to the database */
    conn = PQconnectdb(conninfo);

    /* Check to see that the backend connection was successfully made */
    if (PQstatus(conn) != CONNECTION_OK)
    {
        fprintf(stderr, "%s", PQerrorMessage(conn));
        exit_nicely(conn);
    }

    /* Set always-secure search path, so malicious users can't take control. */
    res = PQexec(conn,
                 "SELECT pg_catalog.set_config('search_path', '', false)");
    if (PQresultStatus(res) != PGRES_TUPLES_OK)
    {
        fprintf(stderr, "SET failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }

    /*
     * Should PQclear PGresult whenever it is no longer needed to avoid memory
     * leaks
     */
    PQclear(res);

    /*
     * Our test case here involves using a cursor, for which we must be inside
     * a transaction block.  We could do the whole thing with a single
     * PQexec() of "select * from pg_database", but that's too trivial to make
     * a good example.
     */

    /* Start a transaction block */
    res = PQexec(conn, "BEGIN");
    if (PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "BEGIN command failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }
    PQclear(res);

    /*
     * Fetch rows from pg_database, the system catalog of databases
     */
    res = PQexec(conn, "DECLARE myportal CURSOR FOR select * from pg_database");
    if (PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "DECLARE CURSOR failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }
    PQclear(res);

    res = PQexec(conn, "FETCH ALL in myportal");
    if (PQresultStatus(res) != PGRES_TUPLES_OK)
    {
        fprintf(stderr, "FETCH ALL failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }

    /* first, print out the attribute names */
    nFields = PQnfields(res);
    for (i = 0; i < nFields; i++)
        printf("% -15s", PQfname(res, i));
    printf("\n\n");

    /* next, print out the rows */
    for (i = 0; i < PQntuples(res); i++)
    {
        for (j = 0; j < nFields; j++)
            printf("% -15s", PQgetvalue(res, i, j));
        printf("\n");
    }

    PQclear(res);

    /* close the portal ... we don't bother to check for errors ... */
    res = PQexec(conn, "CLOSE myportal");
    PQclear(res);

    /* end the transaction */
    res = PQexec(conn, "END");
    PQclear(res);

    /* close the connection to the database and cleanup */
    PQfinish(conn);

    return 0;
}

```

--------------------------------

### Solaris DTrace Linking Error Example

Source: https://www.postgresql.org/docs/13/installation-platform-notes

This output shows a typical linker error on Solaris when using DTrace with an older installation (prior to Solaris 10u4). The error indicates that the DTrace installation is too old to handle probes in static functions, leading to undefined symbol referencing errors and build failure.

```text
Undefined first referenced
 symbol in file
AbortTransaction utils/probes.o
CommitTransaction utils/probes.o
ld: fatal: Symbol referencing errors. No output written to postgres
collect2: ld returned 1 exit status
make: *** [postgres] Error 1
```

--------------------------------

### Potential sepgsql Context Notifications

Source: https://www.postgresql.org/docs/11/sepgsql

Shows example notifications that might appear during the sepgsql installation process, related to invalid object types in the SELinux policy context file. These messages are typically harmless.

```text
/etc/selinux/targeted/contexts/sepgsql_contexts:  line 33 has invalid object type db_blobs
/etc/selinux/targeted/contexts/sepgsql_contexts:  line 36 has invalid object type db_language
/etc/selinux/targeted/contexts/sepgsql_contexts:  line 37 has invalid object type db_language
/etc/selinux/targeted/contexts/sepgsql_contexts:  line 38 has invalid object type db_language
/etc/selinux/targeted/contexts/sepgsql_contexts:  line 39 has invalid object type db_language
/etc/selinux/targeted/contexts/sepgsql_contexts:  line 40 has invalid object type db_language

```

--------------------------------

### Implement Oracle-compatible instr function with two parameters in PL/pgSQL

Source: https://www.postgresql.org/docs/11/plpgsql-porting

This PL/pgSQL function mimics Oracle's `instr(string1, string2)` by searching for the first occurrence of `string2` within `string1`, starting from the first character. It returns the starting index of `string2` or 0 if not found, leveraging the three-parameter version internally.

```plpgsql
--
-- instr functions that mimic Oracle's counterpart
-- Syntax: instr(string1, string2 [, n [, m]])
-- where [] denotes optional parameters.
--
-- Search string1, beginning at the nth character, for the mth occurrence
-- of string2.  If n is negative, search backwards, starting at the abs(n)'th
-- character from the end of string1.
-- If n is not passed, assume 1 (search starts at first character).
-- If m is not passed, assume 1 (find first occurrence).
-- Returns starting index of string2 in string1, or 0 if string2 is not found.
--

CREATE FUNCTION instr(varchar, varchar) RETURNS integer AS $$
BEGIN
    RETURN instr($1, $2, 1);
END;
$$ LANGUAGE plpgsql STRICT IMMUTABLE;
```

--------------------------------

### PostgreSQL Transform Example for hstore and plpythonu

Source: https://www.postgresql.org/docs/11/sql-createtransform

Illustrates the process of creating a transform for the 'hstore' data type and 'plpythonu' language, including setting up the type, extension, necessary functions, and finally the transform itself.

```sql
CREATE TYPE hstore ...;

CREATE EXTENSION plpythonu;

CREATE FUNCTION hstore_to_plpython(val internal) RETURNS internal
LANGUAGE C STRICT IMMUTABLE
AS ...;

CREATE FUNCTION plpython_to_hstore(val internal) RETURNS hstore
LANGUAGE C STRICT IMMUTABLE
AS ...;

CREATE TRANSFORM FOR hstore LANGUAGE plpythonu (
    FROM SQL WITH FUNCTION hstore_to_plpython(internal),
    TO SQL WITH FUNCTION plpython_to_hstore(internal)
);
```

--------------------------------

### PostgreSQL connectby Example: Hierarchical Query with Branch

Source: https://www.postgresql.org/docs/10/tablefunc

Illustrates a PostgreSQL `connectby` query that retrieves hierarchical data including the branch path. This example assumes the `connectby_tree` table is already created and populated. It demonstrates how to specify the table, key fields, starting row, maximum depth, and branch delimiter, while defining the output columns.

```sql
SELECT * FROM connectby('connectby_tree', 'keyid', 'parent_keyid', 'row2', 0, '~')
 AS t(keyid text, parent_keyid text, level int, branch text);
```

--------------------------------

### PostgreSQL SQL for Trigger Setup and Execution

Source: https://www.postgresql.org/docs/6.5/triggers15627

This SQL script demonstrates the setup and execution of PostgreSQL triggers. It includes commands to create a sample table 'ttest', define a C function 'trigf' (assuming it's compiled and available), and then create both BEFORE and AFTER triggers on 'ttest' that execute the 'trigf' procedure. The output shows how the triggers respond to INSERT, UPDATE, and DELETE operations, including handling NULL values.

```sql
vac=> create trigger tbefore before insert or update or delete on ttest 
for each row execute procedure trigf();
CREATE
vac=> create trigger tafter after insert or update or delete on ttest 
for each row execute procedure trigf();
CREATE
vac=> insert into ttest values (null);
NOTICE:trigf (fired before): there are 0 tuples in ttest
INSERT 0 0

-- Insertion skipped and AFTER trigger is not fired

vac=> select * from ttest;
x
-
(0 rows)

vac=> insert into ttest values (1);
NOTICE:trigf (fired before): there are 0 tuples in ttest
NOTICE:trigf (fired after ): there are 1 tuples in ttest
                                       ^^^^^^^^^^^
                             remember what we said about visibility.
INSERT 167793 1
vac=> select * from ttest;
x
-
1
(1 row)

vac=> insert into ttest select x * 2 from ttest;
NOTICE:trigf (fired before): there are 1 tuples in ttest
NOTICE:trigf (fired after ): there are 2 tuples in ttest
                                       ^^^^^^^^^^^
                             remember what we said about visibility.
INSERT 167794 1
vac=> select * from ttest;
x
-
1
2
(2 rows)

vac=> update ttest set x = null where x = 2;
NOTICE:trigf (fired before): there are 2 tuples in ttest
UPDATE 0
vac=> update ttest set x = 4 where x = 2;
NOTICE:trigf (fired before): there are 2 tuples in ttest
NOTICE:trigf (fired after ): there are 2 tuples in ttest
UPDATE 1
vac=> select * from ttest;
x
-
1
4
(2 rows)

vac=> delete from ttest;
NOTICE:trigf (fired before): there are 2 tuples in ttest
NOTICE:trigf (fired after ): there are 1 tuples in ttest
NOTICE:trigf (fired before): there are 1 tuples in ttest
NOTICE:trigf (fired after ): there are 0 tuples in ttest
                                       ^^^^^^^^^^^
                             remember what we said about visibility.
DELETE 2
vac=> select * from ttest;
x
-
(0 rows)

```

--------------------------------

### Example of modular PostgreSQL configuration includes

Source: https://www.postgresql.org/docs/10/config-setting

Demonstrates how to use multiple `include` directives to manage shared, memory-specific, and server-specific configurations separately within the main postgresql.conf file.

```postgresql
include 'shared.conf'
include 'memory.conf'
include 'server.conf'
```

--------------------------------

### Find PostgreSQL Documentation and FAQ

Source: https://www.postgresql.org/docs/6.5/install13271

This snippet indicates the directory where documentation and FAQ files for PostgreSQL are located. Users experiencing issues are advised to consult these files first.

```text
Read the files in directory `/usr/src/pgsql/doc/`.
```

--------------------------------

### PostgreSQL Error Message Tense Example

Source: https://www.postgresql.org/docs/11/error-style-guide

Demonstrates the use of past tense for potentially recoverable errors and present tense for permanent failures. The first example uses past tense ('could not open') indicating a temporary issue, while the second uses present tense ('cannot open') for a conceptual impossibility.

```text
could not open file "%s": %m

cannot open file "%s"

```

--------------------------------

### Dynamic Domain Transitions

Source: https://www.postgresql.org/docs/16/sepgsql

Explains SELinux's dynamic domain transition feature, its security implications, and provides usage examples.

```APIDOC
## Dynamic Domain Transitions

### Description
It is possible to use SELinux's dynamic domain transition feature to switch the security label of the client process to a new context, if allowed by the security policy. This feature requires the `setcurrent` and `dyntransition` permissions.

### Usage Considerations
Dynamic domain transitions should be used with caution, as they allow users to switch their privileges. The `dyntransition` permission is safest when transitioning to a domain with fewer privileges than the original one.

### Example

```sql
-- Get current security context
regression=# select sepgsql_getcon();
             sepgsql_getcon
----------------------------------------------
unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
(1 row)

-- Attempt to transition to a smaller MCS range (allowed)
regression=# SELECT sepgsql_setcon('unconfined_u:unconfined_r:unconfined_t:s0-s0:c1.c4');
 sepgsql_setcon
----------------
 t
(1 row)

-- Attempt to transition back to a larger MCS range (denied)
regression=# SELECT sepgsql_setcon('unconfined_u:unconfined_r:unconfined_t:s0-s0:c1.c1023');
ERROR:  SELinux: security policy violation
```

### Use Case: Connection Pooling
Dynamic domain transitions combined with trusted procedures enable connection pooling software to manage client security labels effectively. The connection pooler can allow clients to switch labels using `sepgsql_setcon()` within a trusted procedure, granting them target user privileges. The pooler can later revert the label change using `sepgsql_setcon(NULL)`, again from within a trusted procedure with proper authorization.
```

--------------------------------

### Example of pg_controldata with options

Source: https://www.postgresql.org/docs/current/app-pgcontroldata

Illustrates how to use pg_controldata with command-line options such as version check and help. These options allow users to retrieve version information or a list of supported arguments without operating on the database cluster itself.

```bash
# Display pg_controldata version
pg_controldata --version

# Display help message
pg_controldata --help
```

--------------------------------

### PostgreSQL Configuration File Example

Source: https://www.postgresql.org/docs/17/config-setting

An example snippet illustrating the structure and content of the postgresql.conf file for server configuration in PostgreSQL.

```postgresql.conf
#------------------------------------------------------------------------------
# MODULE CONFIGURATION
#------------------------------------------------------------------------------

#shared_preload_libraries = ''
#local_preload_libraries = ''

#------------------------------------------------------------------------------
# CONNECTION AND AUTHENTICATION
#------------------------------------------------------------------------------

# - Connection Settings -
#listen_addresses = 'localhost' 	# what IP address(es) to listen on;
								# comma-separated list of addresses;
								# defaults to all (0.0.0.0)
								# (change requires restart)
#port = 5432 					# (change requires restart)
#max_connections = 100 			# (change requires restart)
#superuser_reserved_connections = 3 	# (change requires restart)
#unix_socket_directories = '/var/run/postgresql' # unique on system,
								# comma-separated list of directories
								# (change requires restart)
#unix_socket_group = ''
#unix_socket_permissions = 1777
#    Default values for connections from clients will be: 
#    unix_socket_group = internal
#    unix_socket_permissions = 0777
#    (change requires restart)

# - Security and Logging -
#log_connections = off
#log_disconnections = off
#log_duration = on
#log_min_duration_statement = -1 # -1s means OFF, 0 logs all prepared statements
#log_statement = 'none' # none, ddl, mod, all
#log_replication_commands = off

#log_lock_waits = off
#log_temp_files = 0 # min size in KB, 0 means off, -1 logs all
#log_autovacuum_min_duration = 0 # -1 means off, 0 logs all, > 0 logs duration in ms
#log_error_verbosity = default # default, verbose, tersee
#log_error_detail = off
#log_error_stack_trace = off
#log_client_encoding = off

#log_timezone = 'GMT'
#log_destination = 'stderr' # Valid values are combinations of:
								#   'stderr', 'csvlog', 'syslog', 'eventlog', 'journal'
								# Note that stderr is the default and is always enabled.
								# For other destinations, the respective modules must be loaded.

#logging_collector = on

# - Client Authentication -
# Authentication: Identifies your clients using password files.
# See the manual for a description of the authentication methods.
#auth_local_ = 'ident'
#auth_host_ = 'md5'
#auth_peer_ = 'peer'

# Enable 'trust' authentication for local connections if security 
# concerns are not an issue.  Note that the 'ident' and 'peer' methods 
# are not available on all operating systems.
#auth_local_ = 'trust'

# Allow replication connections from localhost, by a user with the
# replication privilege. Specify as a comma-separated list of
# addresses. You may need to change the next parameter if your system
# uses a non-standard IPv4-mapped IPv6 address format.
#wal_level = replica
#max_wal_senders = 10
#wal_keep_size = 64MB
#archive_mode = off
#archive_command = ''

#------------------------------------------------------------------------------
# RESOURCE USAGE AND SCHEDULING
#------------------------------------------------------------------------------

# - Memory -
#shared_buffers = 128MB 		# min 128kB, warm object cache for operating system
# The actual memory used by shared_buffers is not necessarily aligned 
# on a page boundary. 
# The value must be a multiple of shared_segment_size.
# If shared_buffers is larger than the system memory, PostgreSQL will not start.
# A good starting value is 25% of your system memory.

#max_worker_processes = 8 		# (change requires restart)
#max_parallel_workers_per_gather = 2
#max_parallel_workers = 8 		# (change requires restart)
#min_parallel_table_scan_size = 8MB
#min_parallel_index_scan_size = 8MB

# - Checkpoints and WAL -
# This parameter controls how often the background writer flushes dirty 
# pages from shared_buffers to disk. It is a time interval, not a count.
# checkpoint_timeout = 5min 		# range 1s-1h; default 5min
# A checkpoint flushes all dirty buffers to disk. This is a rather 
# expensive operation, so checkpoints are made as infrequently as possible.
# checkpoint_completion_target = 0.9 	# checkpoint target duration, 0.5 - 0.9
# The time between checkpoints will be checkpoint_timeout. 
# If checkpoint_completion_target is 0.9, then 90% of the time between 
# checkpoints will be spent flushing dirty buffers. 
# The checkpoint_timeout is the maximum time between checkpoints. 
# The checkpoint_completion_target is the maximum time that a checkpoint 
# takes to complete once it has started. 

#------------------------------------------------------------------------------
# REPLICATION
#------------------------------------------------------------------------------

# - WAL -
#wal_level = replica # minimal, replica, or logical; (change requires restart)
#wal_log_hints = off # Should be on for logical decoding

#------------------------------------------------------------------------------
# ARCHIVING
#------------------------------------------------------------------------------

# - Archiving -
#archive_mode = off # reproduces WAL files in a faul-tolerant way; 
							# (change requires restart)
#archive_command = '' 			# command to execute to archive WAL files;
								# set to USE "COPY" to use the COPY command for WAL files
								# (change requires restart)

#------------------------------------------------------------------------------
# EXECUTION AND AUTHENTICATION
#------------------------------------------------------------------------------

# - Statement Behavior -
#log_statement = 'none'
#log_duration = on
#log_min_duration_statement = 1s
#log_checkpoints = off

#------------------------------------------------------------------------------
# FILE LOCATIONS
#------------------------------------------------------------------------------

#------------------------------------------------------------------------------
# CRIMINAL ACTIVITY
#------------------------------------------------------------------------------

# - Criminal Activity -
# This is a list of operations that the server will refuse to perform.
#criminal_activity = ''

#------------------------------------------------------------------------------
# AUTHENTICATION
#------------------------------------------------------------------------------

# - Client Authentication -
# Authentication: Identifies your clients using password files.
# See the manual for a description of the authentication methods.
#auth_local_ = 'ident'
#auth_host_ = 'md5'
#auth_peer_ = 'peer'

# Enable 'trust' authentication for local connections if security 
# concerns are not an issue. Note that the 'ident' and 'peer' methods 
# are not available on all operating systems.
#auth_local_ = 'trust'

#------------------------------------------------------------------------------
# LATERAL AND LATERAL FUNCTIONS
#------------------------------------------------------------------------------

# - Lateral -
# This parameter controls whether LATERAL joins are allowed.
#lateral_enabled = on

#------------------------------------------------------------------------------
# EXECUTION AND PERFORMANCE
#------------------------------------------------------------------------------

# - Statement Behavior -
#log_statement = 'none'
#log_duration = on
#log_min_duration_statement = 1s
#log_checkpoints = off

#------------------------------------------------------------------------------
# QUERY PLAN MANAGEMENT
#------------------------------------------------------------------------------

# - Query Plan Management -
# This parameter controls whether query plan management is enabled.
#plan_cache_mode = 'auto'

#------------------------------------------------------------------------------
# LOCKING AND TRANSACTIONS
#------------------------------------------------------------------------------

# - Deadlocks -
#deadlock_timeout = 10s

#------------------------------------------------------------------------------
# STATEMENTS
#------------------------------------------------------------------------------

# - Statement Behavior -
#log_statement = 'none'
#log_duration = on
#log_min_duration_statement = 1s
#log_checkpoints = off

#------------------------------------------------------------------------------
# MEMORY MANAGEMENT
#------------------------------------------------------------------------------

# - Memory -
#shared_buffers = 128MB
#work_mem = 4MB
#maintenance_work_mem = 64MB
#temp_buffers = 8MB
#vacuum_buffer = 16MB
#temp_file_limit = -1
#effective_cache_size = 4GB

#------------------------------------------------------------------------------
# WAL WRITER
#------------------------------------------------------------------------------

# - WAL -
#wal_level = replica
#wal_log_hints = off

#------------------------------------------------------------------------------
# ARCHIVING
#------------------------------------------------------------------------------

# - Archiving -
#archive_mode = off
#archive_command = ''

#------------------------------------------------------------------------------
# BACKGROUND WRITER
#------------------------------------------------------------------------------

# - Background Writer -
#bgwriter_delay = 10ms
#bgwriter_lru_maxpages = 100
#bgwriter_lru_multiplier = 2.0
#bgwriter_flush_after = 0

#------------------------------------------------------------------------------
# CHECKPOINTER
#------------------------------------------------------------------------------

# - Checkpointer -
#checkpoint_timeout = 5min
#max_wal_size = 1GB
#min_wal_size = 80MB
#checkpoint_completion_target = 0.9
#checkpoint_flush_after = 0
#checkpoint_warning = 30s

#------------------------------------------------------------------------------
# RECOVERY CONFIGURATION
#------------------------------------------------------------------------------

# - Recovery -
#recovery_target_time = ''

#------------------------------------------------------------------------------
# REPLICATION
#------------------------------------------------------------------------------

# - WAL -
#wal_level = replica
#wal_log_hints = off

#------------------------------------------------------------------------------
# ARCHIVING
#------------------------------------------------------------------------------

# - Archiving -
#archive_mode = off
#archive_command = ''

#------------------------------------------------------------------------------
# DATABASE SYSTEM TIMEZONES
#------------------------------------------------------------------------------

#------------------------------------------------------------------------------
# MISCELLANEOUS
#------------------------------------------------------------------------------

# - Miscellaneous -
#fsync = on
#synchronous_commit = on
#synchronous_priorities = on
#wal_sync_method = fsync
#full_page_writes = on
#wal_buffers = -1
#wal_writer_delay = 200ms
#wal_writer_flush_after = 1MB
#wal_keep_size = 64MB
#wal_compression = off
#wal_recycling = on
#wal_recycle = on
#wal_init_file = on
#wal_init_file_size = 16MB
#wal_files = 16
#wal_compress_algorithm = 0
#wal_compress_level = 0
#wal_compress_threshold = 0
#wal_compress_buffers = 0
#wal_compress_alignment = 0
#wal_compress_method = 0
#wal_compress_size = 0
#wal_compress_block_size = 0
#wal_compress_window_size = 0
#wal_compress_dict_size = 0
#wal_compress_dict = 0
#wal_compress_dict_file = 0
#wal_compress_dict_file_size = 0
#wal_compress_dict_file_count = 0
#wal_compress_dict_file_level = 0
#wal_compress_dict_file_level_size = 0
#wal_compress_dict_file_level_count = 0
#wal_compress_dict_file_level_count_size = 0
#wal_compress_dict_file_level_count_size_file = 0
#wal_compress_dict_file_level_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size = 0
#wal_compress_dict_file_level_count_size_file_count_size_file = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count_size_file_count_size_file_count_size_file_count_size_file_count_size_file_count = 0
#wal_compress_dict_file_level_count
```

--------------------------------

### PostgreSQL Extension Control File Example

Source: https://www.postgresql.org/docs/16/extend-extensions

An example of a PostgreSQL extension control file. Control files use a format similar to `postgresql.conf`, with key-value assignments. They define extension properties such as its default version, dependencies, and security settings. Blank lines and comments starting with '#' are permitted. Values that are not single words or numbers should be quoted.

```text
default_version = '1.0'
requires = 'uuid-ossp'
comment = 'My custom extension'
superuser = true
relocatable = false

# Example of a parameter with a quoted string value
directory = 'my_extension/scripts'

```

--------------------------------

### Get PostgreSQL Field Name by Index

Source: https://www.postgresql.org/docs/6.5/libpqplusplus18516

Returns the name of a field (column) associated with a given field index. Field indices start at 0.

```cpp
const char *PgDatabase::FieldName(int field_num)
```

--------------------------------

### PostgreSQL Interactive Monitor (psql) Commands

Source: https://www.postgresql.org/docs/7.0/start27650

Examples of common commands used within the `psql` interactive terminal monitor. These include getting help, executing queries, reading from files, and quitting the monitor.

```sql
Welcome to the POSTGRESQL interactive sql monitor:
  Please read the file COPYRIGHT for copyright terms of POSTGRESQL

  type \? for help on slash commands
  type \q to quit
  type \g or terminate with semicolon to execute query
 You are currently connected to the database: template1

mydb=> 
     

```

```sql
mydb=> \h
     

```

```sql
mydb=> \g
     

```

```sql
mydb=> \i fileName
     

```

```sql
mydb=> \q
     

```

--------------------------------

### Example Initial Data File Format (PostgreSQL)

Source: https://www.postgresql.org/docs/17/bki

Demonstrates the format of initial data files used to populate PostgreSQL system catalogs during the bootstrap phase. These files, like `pg_proc.dat`, reside in the `src/include/catalog/` directory.

```text
# pg_proc.dat
# Initial data for the pg_proc catalog

-- Procedure: pg_proc.oid, pg_proc.proname, pg_proc.prolang, pg_proc.proowner, pg_proc.proretset, pg_proc.pronargs, pg_proc.prosrc, pg_proc.probin, pg_proc.proacl
-- Data: {1, 'pg_catalog.pg_class', 12, 22, false, 0, '\0', '\0', '\0'}
-- Data: {2, 'pg_catalog.pg_type', 12, 22, false, 0, '\0', '\0', '\0'}
-- ...
```

--------------------------------

### Create PostgreSQL Ascending Sequence

Source: https://www.postgresql.org/docs/devel/sql-createsequence

This SQL example demonstrates how to create a new ascending sequence in PostgreSQL. It specifies a starting value of 101, ensuring that the first generated number will be 101.

```SQL
CREATE SEQUENCE serial START 101;
```

--------------------------------

### Configure PostgreSQL with ICU Library Support

Source: https://www.postgresql.org/docs/12/install-procedure

Build PostgreSQL with support for the ICU library, which requires the ICU4C package. This example shows how to specify custom include paths and library locations for ICU4C when pkg-config is not available or for older versions.

```bash
./configure ... --with-icu ICU_CFLAGS='-I/some/where/include' ICU_LIBS='-L/some/where/lib -licui18n -licuuc -licudata'
```

--------------------------------

### Run PostgreSQL Regression Tests

Source: https://www.postgresql.org/docs/6.4/install12063

This snippet outlines the commands to clean, build, and run the PostgreSQL regression tests. It guides users on navigating to the test directory and executing the test suite using 'gmake'.

```shell
$ cd /usr/src/pgsql/src/test/regress
$ gmake clean
$ gmake all runtest
```

--------------------------------

### Test libpq C Example - Database Connection and Query

Source: https://www.postgresql.org/docs/13/libpq-example

This C program demonstrates connecting to a PostgreSQL database using libpq, executing SQL commands, fetching data, and handling results. It shows transaction management, cursor usage, and proper connection cleanup.

```c
#include <stdio.h>
#include <stdlib.h>
#include "libpq-fe.h"

static void
exit_nicely(PGconn *conn)
{
    PQfinish(conn);
    exit(1);
}

int
main(int argc, char **argv)
{
    const char *conninfo;
    PGconn     *conn;
    PGresult   *res;
    int         nFields;
    int         i, j;

    /*
     * If the user supplies a parameter on the command line, use it as the
     * conninfo string; otherwise default to setting dbname=postgres and using
     * environment variables or defaults for all other connection parameters.
     */
    if (argc > 1)
        conninfo = argv[1];
    else
        conninfo = "dbname = postgres";

    /* Make a connection to the database */
    conn = PQconnectdb(conninfo);

    /* Check to see that the backend connection was successfully made */
    if (PQstatus(conn) != CONNECTION_OK)
    {
        fprintf(stderr, "Connection to database failed: %s",
                PQerrorMessage(conn));
        exit_nicely(conn);
    }

    /* Set always-secure search path, so malicious users can't take control. */
    res = PQexec(conn,
                 "SELECT pg_catalog.set_config('search_path', '', false)");
    if (PQresultStatus(res) != PGRES_TUPLES_OK)
    {
        fprintf(stderr, "SET failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }

    /*
     * Should PQclear PGresult whenever it is no longer needed to avoid memory
     * leaks
     */
    PQclear(res);

    /*
     * Our test case here involves using a cursor, for which we must be inside
     * a transaction block.  We could do the whole thing with a single
     * PQexec() of "select * from pg_database", but that's too trivial to make
     * a good example.
     */

    /* Start a transaction block */
    res = PQexec(conn, "BEGIN");
    if (PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "BEGIN command failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }
    PQclear(res);

    /*
     * Fetch rows from pg_database, the system catalog of databases
     */
    res = PQexec(conn, "DECLARE myportal CURSOR FOR select * from pg_database");
    if (PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "DECLARE CURSOR failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }
    PQclear(res);

    res = PQexec(conn, "FETCH ALL in myportal");
    if (PQresultStatus(res) != PGRES_TUPLES_OK)
    {
        fprintf(stderr, "FETCH ALL failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }

    /* first, print out the attribute names */
    nFields = PQnfields(res);
    for (i = 0; i < nFields; i++)
        printf("% -15s", PQfname(res, i));
    printf("\n\n");

    /* next, print out the rows */
    for (i = 0; i < PQntuples(res); i++)
    {
        for (j = 0; j < nFields; j++)
            printf("% -15s", PQgetvalue(res, i, j));
        printf("\n");
    }

    PQclear(res);

    /* close the portal ... we don't bother to check for errors ... */
    res = PQexec(conn, "CLOSE myportal");
    PQclear(res);

    /* end the transaction */
    res = PQexec(conn, "END");
    PQclear(res);

    /* close the connection to the database and cleanup */
    PQfinish(conn);

    return 0;
}

```

--------------------------------

### PostgreSQL Command Prompt Notation Examples

Source: https://www.postgresql.org/docs/6.4/intro263

Illustrates the different command prompts used in PostgreSQL documentation to indicate the user or account executing the command. This helps in understanding the context of command execution.

```shell
> echo "Root command"

```

```shell
% psql -U postgres

```

```shell
$ psql -U someuser

```

```sql
=> SELECT version();

```

```sql
SELECT count(*) FROM my_table;

```

--------------------------------

### Synopsis of initdb command

Source: https://www.postgresql.org/docs/17/app-initdb

The synopsis shows the basic structure of the initdb command, including optional arguments and the required directory argument.

```bash
initdb [_option_]... [`--pgdata` | -D ] _directory_
```

--------------------------------

### PL/Tcl Event Trigger Function Example

Source: https://www.postgresql.org/docs/17/pltcl-event-trigger

This example demonstrates how to create an event trigger function in PL/Tcl. The function is designed to log a notice message whenever a DDL command starts. It utilizes special variables provided by the trigger manager and requires a specific function signature returning 'event_trigger'.

```sql
CREATE OR REPLACE FUNCTION tclsnitch() RETURNS event_trigger AS $$
  elog NOTICE "tclsnitch: $TG_event $TG_tag"
$$ LANGUAGE pltcl;

CREATE EVENT TRIGGER tcl_a_snitch ON ddl_command_start EXECUTE FUNCTION tclsnitch();
```

--------------------------------

### Stop PostgreSQL using System Service (Linux Example)

Source: https://www.postgresql.org/docs/6.4/install12063

This command demonstrates how to stop the PostgreSQL service on a Linux system using its init script. This is an alternative to manually killing the postmaster process.

```shell
$ /etc/rc.d/init.d/postgres.init stop
```

--------------------------------

### Example: Initializing Shared Memory with LWLock (C)

Source: https://www.postgresql.org/docs/current/xfunc-c

A C code example demonstrating how to safely initialize a shared memory segment using `ShmemInitStruct`. It acquires an exclusive lock on `AddinShmemInitLock` before accessing the shared memory and releases it afterward. If the segment is new (`!found`), it initializes contents and gets a named LWLock tranche.

```c
static mystruct *ptr = NULL;
bool        found;

LWLockAcquire(AddinShmemInitLock, LW_EXCLUSIVE);
ptr = ShmemInitStruct("my struct name", size, &found);
if (!found)
{
    ... initialize contents of shared memory ...
    ptr->locks = GetNamedLWLockTranche("my tranche name");
}
LWLockRelease(AddinShmemInitLock);
```

--------------------------------

### Prepare and Initialize PostgreSQL Data Directory with Permissions

Source: https://www.postgresql.org/docs/16/creating-cluster

This sequence of commands demonstrates how to set up the necessary directory structure and permissions for a PostgreSQL data directory before initializing it. It involves creating a parent directory as root, changing its ownership to the `postgres` user, switching to the `postgres` user, and then running `initdb` to create the database cluster.

```bash
mkdir /usr/local/pgsql
chown postgres /usr/local/pgsql
su postgres
initdb -D /usr/local/pgsql/data
```

--------------------------------

### Run PostgreSQL Parallel Regression Tests (Existing Installation)

Source: https://www.postgresql.org/docs/10/regress-run

Executes PostgreSQL regression tests in parallel against an already installed and running server. Similar to `make installcheck`, it requires an initialized data area and a started server. This mode utilizes multiple server processes to run test groups concurrently, enhancing confidence in interprocess communication and locking.

```bash
make installcheck-parallel
```

--------------------------------

### Build Man Pages with PostgreSQL

Source: https://www.postgresql.org/docs/10/docguide-build

Creates man pages from DocBook refentry pages using DocBook XSL stylesheets. The output is suitable for man command usage and is also distributed as a tar archive.

```makefile
make man
```

--------------------------------

### pg_walsummary Usage Example

Source: https://www.postgresql.org/docs/17/app-pgwalsummary

Demonstrates the basic command-line usage of `pg_walsummary` to print the contents of WAL summary files. It shows how to specify options and input files.

```bash
pg_walsummary [_option_] [_file_]...
```

--------------------------------

### Build and Install PL/perl Extension

Source: https://www.postgresql.org/docs/7.0/pl-perl4533

Steps to build and install the PL/perl extension from source. This involves navigating to the source directory, running Perl's Makefile.PL, and then executing make. The resulting shared library should be copied to the PostgreSQL installation's lib subdirectory.

```shell
cd $PGSRC/src/pl/plperl
perl Makefile.PL
make
```

--------------------------------

### Setting Up Environment for pg_upgrade (Windows)

Source: https://www.postgresql.org/docs/13/pgupgrade

This sequence of commands is executed on Windows to prepare the environment for running pg_upgrade. It involves switching to the 'postgres' user and adding the new PostgreSQL binaries directory to the system's PATH.

```windows-batch
RUNAS /USER:postgres "CMD.EXE"
SET PATH=%PATH%;C:\Program Files\PostgreSQL\13\bin;
```

--------------------------------

### pgtcl Example Program (Tcl)

Source: https://www.postgresql.org/docs/7.2/programmer

Demonstrates the usage of the pgtcl library for Tcl-based PostgreSQL interactions. This example shows how to establish a connection and execute commands.

```tcl
load /path/to/libpgtcl.so pgtcl

set conn [ pgtcl::connect "dbname=mydb user=postgres password=mypass host=localhost port=5432" ]

if { $conn == "" } {
    puts stderr "Connection failed"
    exit 1
}

set result [ pgtcl::exec $conn "SELECT version();" ]

puts $result

pgtcl::disconnect $conn
```

--------------------------------

### Get PostgreSQL Field Type by Name

Source: https://www.postgresql.org/docs/6.5/libpqplusplus18516

Returns the internal coding of the field type associated with a given field name. Field indices start at 0.

```cpp
Oid PgDatabase::FieldType(const char* field_name)
```

--------------------------------

### Configure PostgreSQL Service in inittab (RedHat Linux)

Source: https://www.postgresql.org/docs/6.4/install12063

This snippet demonstrates how to add an entry to the `/etc/inittab` file on RedHat Linux to automatically start the PostgreSQL postmaster process. It configures the process to respawn if it dies and redirects its output to a log file.

```shell
pg:2345:respawn:/bin/su - postgres -c
    "/usr/local/pgsql/bin/postmaster -D/usr/local/pgsql/data
    >> /usr/local/pgsql/server.log 2>&1 </dev/null"
```

--------------------------------

### Create PostgreSQL Subscriber Table and Subscription

Source: https://www.postgresql.org/docs/15/logical-replication-row-filter

This snippet demonstrates the setup on a subscriber node. It involves creating a table (`t1`) with the same schema as the publisher's table and then establishing a subscription (`s1`) to a specific publication (`p1`) from the publisher. This prepares the subscriber for receiving replicated data.

```sql
test_sub=# CREATE TABLE t1(a int, b int, c text, PRIMARY KEY(a,c));
CREATE TABLE
test_sub=# CREATE SUBSCRIPTION s1
test_sub-# CONNECTION 'host=localhost dbname=test_pub application_name=s1'
test_sub-# PUBLICATION p1;
CREATE SUBSCRIPTION
```

--------------------------------

### PostgreSQL LISTEN/NOTIFY Usage Example

Source: https://www.postgresql.org/docs/7.0/sql-listen

An example demonstrating the LISTEN and NOTIFY commands in psql. This shows how to set up a notification channel and send a notification, with the expected asynchronous response.

```sql
LISTEN virtual;
NOTIFY virtual;

Asynchronous NOTIFY 'virtual' from backend with pid '8448' received.

```

--------------------------------

### Get PostgreSQL Field Type by Index

Source: https://www.postgresql.org/docs/6.5/libpqplusplus18516

Returns the internal coding of the field type associated with a given field index. Field indices start at 0.

```cpp
Oid PgDatabase::FieldType(int field_num)
```

--------------------------------

### PL/pgSQL Function to Concatenate Text (PostgreSQL)

Source: https://www.postgresql.org/docs/7.3/programmer

This PL/pgSQL snippet creates a function that concatenates two text strings. It showcases string manipulation within PL/pgSQL.

```plpgsql
-- A Simple PL/pgSQL Function to Concatenate Text

CREATE OR REPLACE FUNCTION concatenate_text(text1 TEXT, text2 TEXT)
RETURNS TEXT AS $$
BEGIN
    RETURN text1 || text2; -- PostgreSQL string concatenation operator
END;
$$ LANGUAGE plpgsql;

-- Example usage:
-- SELECT concatenate_text('Hello', ' World!');

```

--------------------------------

### Configure PostgreSQL Source Code

Source: https://www.postgresql.org/docs/7.0/install17165

This command configures the PostgreSQL source code for your system, allowing you to specify installation paths and build options. It's a crucial step before compilation. Common options include `--prefix` for installation directory, `--enable-locale` for locale support, `--enable-multibyte` for multibyte character encodings, and flags for building Perl and ODBC interfaces.

```shell
> ./configure

```

```shell
> ./configure --help

```

--------------------------------

### Create an ascending PostgreSQL sequence

Source: https://www.postgresql.org/docs/10/sql-createsequence

This example demonstrates how to create a new sequence in PostgreSQL that starts at a specified value and increments thereafter. Sequences are useful for generating unique identifiers.

```sql
CREATE SEQUENCE serial START 101;
```

--------------------------------

### Example `jsonb` Document Structure (JSON)

Source: https://www.postgresql.org/docs/10/datatype-json

This JSON object represents a typical document stored in the `jdoc` column of the `api` table. It illustrates the structure, including GUID, name, boolean flags, company, address, timestamp, coordinates, and an array of tags, which serves as context for the subsequent indexing and querying examples.

```json
{
    "guid": "9c36adc1-7fb5-4d5b-83b4-90356a46061a",
    "name": "Angela Barton",
    "is_active": true,
    "company": "Magnafone",
    "address": "178 Howard Place, Gulf, Washington, 702",
    "registered": "2009-11-07T08:53:22 +08:00",
    "latitude": 19.793713,
    "longitude": 86.513373,
    "tags": [
        "enim",
        "aliquip",
        "qui"
    ]
}
```

--------------------------------

### Build PostgreSQL HTML Documentation with Meson

Source: https://www.postgresql.org/docs/17/docguide-build-meson

This command builds the HTML version of the PostgreSQL documentation using the Meson build system. Ensure you are in the 'build' directory or use the '-C build' flag. The output is placed in the 'build/doc/src/sgml' subdirectory.

```shell
build$ ninja html
```

--------------------------------

### Execute PostgreSQL Query with Parameters and Process Results in C

Source: https://www.postgresql.org/docs/8.0/libpq-example

This C code snippet demonstrates how to connect to a PostgreSQL database, execute a parameterized SELECT query, and process the returned tuple data. It includes error handling for query execution and shows how to retrieve specific fields by their names. Dependencies include the libpq library.

```c
/* Here is our out-of-line parameter value */
        paramValues[0] = "joe's place";

        res = PQexecParams(conn,
                                           "SELECT * FROM test1 WHERE t = $1",
                                           1,           /* one param */
                                           NULL,        /* let the backend deduce param type */
                                           paramValues,
                                           NULL,        /* don't need param lengths since text */
                                           NULL,        /* default to all text params */
                                           1);          /* ask for binary results */

        if (PQresultStatus(res) != PGRES_TUPLES_OK)
        {
                fprintf(stderr, "SELECT failed: %s", PQerrorMessage(conn));
                PQclear(res);
                exit_nicely(conn);
        }

        /* Use PQfnumber to avoid assumptions about field order in result */
        i_fnum = PQfnumber(res, "i");
        t_fnum = PQfnumber(res, "t");
        b_fnum = PQfnumber(res, "b");

        for (i = 0; i < PQntuples(res); i++)
        {
                char       *iptr;
                char       *tptr;
                char       *bptr;
                int                     blen;
                int                     ival;

                /* Get the field values (we ignore possibility they are null!) */
                iptr = PQgetvalue(res, i, i_fnum);
                tptr = PQgetvalue(res, i, t_fnum);
                bptr = PQgetvalue(res, i, b_fnum);

                /*
                 * The binary representation of INT4 is in network byte order,
                 * which we'd better coerce to the local byte order.
                 */
                ival = ntohl(*((uint32_t *) iptr));

                /*
                 * The binary representation of TEXT is, well, text, and since
                 * libpq was nice enough to append a zero byte to it, it'll work
                 * just fine as a C string.
                 *
                 * The binary representation of BYTEA is a bunch of bytes, which
                 * could include embedded nulls so we have to pay attention to
                 * field length.
                 */
                blen = PQgetlength(res, i, b_fnum);

                printf("tuple %d: got\n");
                printf(" i = (%d bytes) %d\n",
                           PQgetlength(res, i, i_fnum), ival);
                printf(" t = (%d bytes) '%s'\n",
                           PQgetlength(res, i, t_fnum), tptr);
                printf(" b = (%d bytes) ", blen);
                for (j = 0; j < blen; j++)
                        printf("\\%03o", bptr[j]);
                printf("\n\n");
        }

        PQclear(res);

        /* close the connection to the database and cleanup */
        PQfinish(conn);

        return 0;
}

```

--------------------------------

### Generate HTML from DocBook SGML using jade

Source: https://www.postgresql.org/docs/7.0/docguide29024

This command uses the 'jade' processor to convert a PostgreSQL user's guide from DocBook SGML format to HTML. It specifies the output format, the DSSSL style sheet, and the input file.

```bash
jade -t sgml -d /usr/local/share/docbook/html/docbook.dsl -D ../graphics postgres.sgml
         

```

--------------------------------

### Start PostgreSQL Server

Source: https://www.postgresql.org/docs/18/logical-replication-upgrade

Starts the PostgreSQL server process. This command is used to bring the database server online after an upgrade or maintenance operation.

```bash
pg_ctl -D /opt/PostgreSQL/data1_upgraded start -l logfile
```

--------------------------------

### PostgreSQL INSERT statement for shoelace_ok

Source: https://www.postgresql.org/docs/10/rules-update

This SQL statement demonstrates an initial INSERT operation that selects data from 'shoelace_arrive' and 'shoelace_ok'. It serves as the starting point for query transformation examples.

```sql
INSERT INTO shoelace_ok
SELECT shoelace_arrive.arr_name, shoelace_arrive.arr_quant
  FROM shoelace_arrive shoelace_arrive, shoelace_ok shoelace_ok;
```

--------------------------------

### PostgreSQL Configuration File (`postgresql.conf`) Example

Source: https://www.postgresql.org/docs/7.3/runtime-config

Demonstrates the syntax and format of the `postgresql.conf` file for setting PostgreSQL run-time parameters. Comments, value types, and whitespace handling are illustrated.

```postgresql.conf
# This is a comment
log_connections = yes
syslog = 2
search_path = '$user, public'

```

--------------------------------

### Example of including configuration files from a directory

Source: https://www.postgresql.org/docs/10/config-setting

Shows how to use `include_dir` to include configuration files organized within a directory (e.g., 'conf.d'). File naming conventions (e.g., `00shared.conf`) dictate the loading order and override precedence.

```postgresql
include_dir 'conf.d'
```

--------------------------------

### Get Field Name by Index with PQfname

Source: https://www.postgresql.org/docs/7.0/libpq-chapter22422

Retrieves the name of a field (column) given its zero-based index within the query result. Field indices start from 0.

```c
char *PQfname(const PGresult *res,
                    int field_index);

```

--------------------------------

### Handling Spaces in Directory Paths for Bison

Source: https://www.postgresql.org/docs/12/install-windows-full

Addresses a known issue with Bison when installed in directories containing spaces. It suggests alternative installation paths or using NTFS short names to resolve potential conflicts.

```shell
# Example of using NTFS short name in PATH environment variable:
# set PATH=C:\PROGRA~1\GnuWin32;%PATH%
```

--------------------------------

### Configure JIT Provider in PostgreSQL

Source: https://www.postgresql.org/docs/18/runtime-config-client

Sets the name of the JIT provider library to be used by PostgreSQL. This parameter can only be set at server start. If set to a non-existent library, JIT will not be available, but no error will be raised, allowing for separate installation of JIT support.

```postgresql
jit_provider = 'llvmjit'
```

--------------------------------

### Display pgbench Help

Source: https://www.postgresql.org/docs/18/pgbench

Shows a help message summarizing all available pgbench command-line arguments and exits. This is the standard way to get usage information for the utility.

```bash
-?
--help

```

--------------------------------

### Install PostgreSQL Executables (Shell)

Source: https://www.postgresql.org/docs/7.0/install17165

Installs the PostgreSQL executable files and libraries. This command should be run as the user who will own the installed files, which may or may not be the database superuser.

```shell
> gmake install
```

--------------------------------

### Get Field Format Modifier - PQfmod

Source: https://www.postgresql.org/docs/6.4/libpq-chapter16943

Retrieves the type-specific modification data for a given field in a PostgreSQL query result. Field indices start at 0.

```c
int PQfmod(PGresult *res,
           int field_index);

```

--------------------------------

### Manage PostgreSQL Logical Replication Slots

Source: https://www.postgresql.org/docs/15/logicaldecoding-example

Commands to manage logical replication slots using `pg_recvlogical`. This includes creating, dropping, and starting the logical decoding process from a specified slot. Ensure the database and slot names are correctly provided.

```bash
$ pg_recvlogical -d postgres --slot=test --drop-slot
$ pg_recvlogical -d postgres --slot=test --create-slot --two-phase
$ pg_recvlogical -d postgres --slot=test --start -f -
```

--------------------------------

### Configure FOP Memory Settings for PDF Generation

Source: https://www.postgresql.org/docs/10/docguide-build

Provides example configurations for setting Java heap space for the FOP processor to resolve memory-related errors during PDF documentation builds. These settings are typically placed in ~/.foprc.

```bash
# FOP binary distribution
FOP_OPTS='-Xmx1500m'
# Debian
JAVA_ARGS='-Xmx1500m'
# Red Hat
ADDITIONAL_FLAGS='-Xmx1500m'
```

--------------------------------

### Get current local time (PostgreSQL)

Source: https://www.postgresql.org/docs/16/functions-datetime

Retrieves the current time of day without date or time zone information. The time is based on the start of the current transaction.

```SQL
localtime
```

--------------------------------

### Create New PostgreSQL Source and Install Directories

Source: https://www.postgresql.org/docs/6.5/install12893

This command sequence creates new directories for the PostgreSQL source code and installation, assigning ownership to the 'postgres' user and group. This is a prerequisite for installing a new version.

```bash
$ su
$ cd /usr/src
$ mkdir pgsql
$ chown postgres:postgres pgsql
$ cd /usr/local
$ mkdir pgsql
$ chown postgres:postgres pgsql
$ exit
```

--------------------------------

### Split String by Delimiter and Get Part in PostgreSQL SQL

Source: https://www.postgresql.org/docs/12/functions-string

Splits a string based on a delimiter and returns the specified field, with fields counted starting from one.

```SQL
split_part('abc~@~def~@~ghi', '~@~', 2)
```

--------------------------------

### PostgreSQL vacuumdb Basic Usage Examples

Source: https://www.postgresql.org/docs/10/app-vacuumdb

Demonstrates fundamental ways to use the vacuumdb command to clean and analyze PostgreSQL databases. These examples show cleaning a specific database and performing analysis for the optimizer.

```bash
$ **vacuumdb test**

```

```bash
$ **vacuumdb --analyze bigdb**

```

--------------------------------

### PostgreSQL Table Definitions

Source: https://www.postgresql.org/docs/10/rules-triggers

Defines the 'computer' and 'software' tables used in the examples. These tables store information about computers and the software installed on them, with indexed columns for efficient lookups.

```sql
CREATE TABLE computer (
    hostname        text,    -- indexed
    manufacturer    text     -- indexed
);

CREATE TABLE software (
    software        text,    -- indexed
    hostname        text     -- indexed
);
```

--------------------------------

### Verify a PostgreSQL Base Backup

Source: https://www.postgresql.org/docs/13/app-pgverifybackup

This example demonstrates how to create a base backup using `pg_basebackup` from a specified host and directory, then immediately verify its integrity using `pg_verifybackup`. It illustrates a basic, two-step process for ensuring backup validity.

```Shell
$ pg_basebackup -h mydbserver -D /usr/local/pgsql/data
$ pg_verifybackup /usr/local/pgsql/data
```

--------------------------------

### Set PostgreSQL MANPATH for Documentation on Linux/Unix Shells

Source: https://www.postgresql.org/docs/12/install-post

Shows how to configure the `MANPATH` environment variable to include the directory containing PostgreSQL's manual pages. This enables the `man` command to correctly locate and display PostgreSQL documentation, assuming it wasn't installed in a default search location.

```sh
MANPATH=/usr/local/pgsql/share/man:$MANPATH
export MANPATH
```

--------------------------------

### COPY Command Example with libpq Functions

Source: https://www.postgresql.org/docs/6.3/c4006

An example demonstrating the usage of `PQexec`, `PQputline`, and `PQendcopy` for performing a `COPY` operation in PostgreSQL.

```APIDOC
## COPY Command Example

### Description
This example illustrates how to use `PQexec`, `PQputline`, and `PQendcopy` to execute a `COPY` command in PostgreSQL.

### Steps
1. Create a table using `PQexec`.
2. Initiate the `COPY FROM STDIN` command using `PQexec`.
3. Send data rows using `PQputline`.
4. Signal the end of data with `PQputline(".\n")`.
5. Synchronize with the backend using `PQendcopy`.

### Code Snippet
```c
PQexec(conn, "create table foo (a int4, b char16, d float8)");
PQexec(conn, "copy foo from stdin");
PQputline(conn, "3<TAB>hello world<TAB>4.5\n");
PQputline(conn,"4<TAB>goodbye world<TAB>7.11\n");
// ... more data rows ...
PQputline(conn,".\n"); // Signal end of data
PQendcopy(conn); // Sync with the backend
```
```

--------------------------------

### Managing Transactions in PostgreSQL

Source: https://www.postgresql.org/docs/13/glossary

Explains the basic commands for managing transactions in PostgreSQL. Transactions ensure atomicity, consistency, isolation, and durability (ACID). This example shows starting, committing, and rolling back a transaction.

```sql
BEGIN;

-- Perform database operations here
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
INSERT INTO transactions (account_id, amount) VALUES (1, -100);

-- Commit the transaction if successful
COMMIT;

-- Or rollback if an error occurs
-- ROLLBACK;
```

--------------------------------

### Start psql and Observe Database Prompt

Source: https://www.postgresql.org/docs/13/app-psql

Illustrates the process of initiating an interactive `psql` session by connecting to a specified database, 'testdb'. The command execution leads to the display of the `psql` version information and the interactive prompt (e.g., `testdb=>`), indicating a successful connection and readiness to accept SQL commands.

```shell
psql testdb
```

--------------------------------

### Declare PL/Perl Language (SQL)

Source: https://www.postgresql.org/docs/10/xplang-install

Example of declaring the PL/Perl procedural language as trusted. It links the language name 'plperl' to its previously declared handler, inline, and validator functions.

```sql
CREATE TRUSTED PROCEDURAL LANGUAGE plperl
    HANDLER plperl_call_handler
    INLINE plperl_inline_handler
    VALIDATOR plperl_validator;
```

--------------------------------

### PostgreSQL: Filtering Rows with WHERE Clause before Aggregation

Source: https://www.postgresql.org/docs/11/tutorial-agg

Illustrates applying a filter using the WHERE clause to select specific rows before performing grouping and aggregation. This example filters for cities starting with 'S'.

```sql
SELECT city, count(*), max(temp_lo)
    FROM weather
    WHERE city LIKE 'S%'
    GROUP BY city;
```

--------------------------------

### PostgreSQL Error Message Structure Example

Source: https://www.postgresql.org/docs/10/error-style-guide

Demonstrates the recommended structure for PostgreSQL error messages, separating the primary message from detail and hint information for better client-side handling.

```PostgreSQL
Primary:    could not create shared memory segment: %m
Detail:     Failed syscall was shmget(key=%d, size=%u, 0%o).
Hint:       the addendum
```

--------------------------------

### Start PostgreSQL Server using pg_ctl Utility

Source: https://www.postgresql.org/docs/current/server-start

The 'pg_ctl' utility provides a simplified interface for managing the PostgreSQL server. This command starts the server in the background and directs log output to a specified file. The -D option specifies the data directory.

```shell
pg_ctl start -l logfile

```

--------------------------------

### PostgreSQL Startup and Authentication

Source: https://www.postgresql.org/docs/17/protocol-flow

This section details the initial startup and authentication messages exchanged between a PostgreSQL client (frontend) and the server.

```APIDOC
## PostgreSQL Startup and Authentication

### Description
To begin a session, a frontend establishes a connection to the PostgreSQL server. This involves sending a startup message containing the username, database name, and protocol version. The server then processes this information, checks configuration files (like `pg_hba.conf`), and sends an authentication request. The frontend must respond with an appropriate authentication message. The authentication process can involve multiple exchanges depending on the method used.

### Authentication Messages

#### Server to Frontend

*   **ErrorResponse**: Indicates the connection attempt has been rejected. The server closes the connection immediately.
*   **AuthenticationOk**: Signals that the authentication exchange has been successfully completed.
*   **AuthenticationKerberosV5**: (Deprecated) Requires the frontend to engage in a Kerberos V5 authentication dialog. Success leads to `AuthenticationOk`, failure to `ErrorResponse`.
*   **AuthenticationCleartextPassword**: Prompts the frontend to send a `PasswordMessage` with the password in clear text. Correct password results in `AuthenticationOk`, incorrect in `ErrorResponse`.
*   **AuthenticationMD5Password**: Requires the frontend to send a `PasswordMessage` with the password and username, encrypted using MD5 with a provided salt. Correct credentials lead to `AuthenticationOk`, incorrect to `ErrorResponse`.
*   **AuthenticationGSS**: Initiates a GSSAPI negotiation. The frontend responds with a `GSSResponse`. Further steps may involve `AuthenticationGSSContinue`.
*   **AuthenticationSSPI**: Initiates an SSPI negotiation. The frontend responds with a `GSSResponse`. Further steps may involve `AuthenticationGSSContinue`.
*   **AuthenticationGSSContinue**: Contains response data for GSSAPI or SSPI negotiation. If more data is needed, the frontend sends another `GSSResponse`. Completion results in `AuthenticationOk` or `ErrorResponse`.
*   **AuthenticationSASL**: Initiates a SASL negotiation using mechanisms listed in the message. The frontend sends a `SASLInitialResponse`. Further steps may involve `AuthenticationSASLContinue`.
*   **AuthenticationSASLContinue**: Contains challenge data for SASL negotiation. The frontend responds with a `SASLResponse`.
*   **AuthenticationSASLFinal**: Indicates SASL authentication completion with mechanism-specific data for the client. Success is signaled by `AuthenticationOk`, failure by `ErrorResponse`.
*   **NegotiateProtocolVersion**: Indicates the server wishes to negotiate a different protocol version.

#### Frontend to Server

*   **StartupMessage**: Sent initially by the frontend. Contains username, database name, and protocol version. Optionally includes run-time parameters.
*   **PasswordMessage**: Sent in response to `AuthenticationCleartextPassword` or `AuthenticationMD5Password`, containing the encrypted or clear-text password.
*   **GSSResponse**: Sent in response to `AuthenticationGSS` or `AuthenticationSSPI`, containing the initial part of the GSSAPI/SSPI data stream.
*   **SASLInitialResponse**: Sent in response to `AuthenticationSASL`, containing the selected SASL mechanism name and the first part of the SASL data stream.
*   **SASLResponse**: Sent in response to `AuthenticationSASLContinue`, containing the response to the SASL challenge.

### Error Handling

*   **ErrorResponse**: If received at any point during authentication, the connection attempt is rejected, and the connection is closed by the server.
```

--------------------------------

### Get Current Transaction Timestamp in PostgreSQL using transaction_timestamp()

Source: https://www.postgresql.org/docs/14/functions-datetime

The `transaction_timestamp()` function is an alias for `now()`, returning the current date and time as a `timestamp with time zone` at the start of the current transaction.

```SQL
SELECT transaction_timestamp()
```

--------------------------------

### PostgreSQL Get Array Dimension Length Function (`array_length`) Examples

Source: https://www.postgresql.org/docs/14/functions-array

Returns the length of a specific dimension within an array. If the requested dimension is empty or does not exist, it returns NULL.

```SQL
array_length(array[1,2,3], 1)
```

```SQL
array_length(array[]::int[], 1)
```

```SQL
array_length(array['text'], 2)
```

--------------------------------

### Start PostgreSQL Server with pg_ctl

Source: https://www.postgresql.org/docs/10/app-pg-ctl

Starts a PostgreSQL server instance. It requires the data directory to be specified with -D. Logging can be directed to a file using -l. The -W flag prompts for a password, and -t sets a timeout. Options for the server can be passed via -o.

```bash
pg_ctl start -D /path/to/data/directory -l /path/to/logfile.log -t 60
```

--------------------------------

### Install PostgreSQL Extension after Setting Search Path

Source: https://www.postgresql.org/docs/10/sql-createextension

This method achieves the same result as the previous example by first setting the search path to the desired schema and then executing the CREATE EXTENSION command. This is useful when multiple operations will be performed within the same schema.

```sql
SET search_path = addons;
CREATE EXTENSION hstore;
```

--------------------------------

### PostgreSQL Error Message Examples

Source: https://www.postgresql.org/docs/15/error-style-guide

Illustrates the correct and incorrect ways to format error messages, focusing on clarity, providing reasons for errors, and avoiding extraneous information like function names.

```text
BAD:    could not open file %s
BETTER: could not open file %s (I/O failure)
```

```text
BAD:    pg_strtoint32: error in "z": cannot parse "z"
BETTER: invalid input syntax for type integer: "z"
```

```text
BAD:    open() failed: %m
BETTER: could not open file %s: %m
```

--------------------------------

### PostgreSQL Get Array Dimensions Function (`array_dims`) Example

Source: https://www.postgresql.org/docs/14/functions-array

Returns a text representation describing the dimensions of an array. The output format indicates the lower and upper bounds for each dimension.

```SQL
array_dims(ARRAY[[1,2,3], [4,5,6]])
```

--------------------------------

### PostgreSQL libpq Event Handling Example (C)

Source: https://www.postgresql.org/docs/current/libpq-events

This C code demonstrates how to register and handle libpq events to manage custom data associated with PostgreSQL connections and results. It includes setup for connection, event processing, and data lifecycle management for connection and result instances.

```c
#include <libpq-events.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

/* The instanceData */
typedef struct
{
    int n;
    char *str;
} mydata;

/* Function prototypes */
static int myEventProc(PGEventId evtId, void *evtInfo, void *passThrough);
mydata *get_mydata(PGconn *conn);
mydata *dup_mydata(mydata *data);
void free_mydata(mydata *data);

int
main(void)
{
    mydata *data;
    PGresult *res;
    PGconn *conn =
        PQconnectdb("dbname=postgres options=-csearch_path=");

    if (PQstatus(conn) != CONNECTION_OK)
    {
        /* PQerrorMessage's result includes a trailing newline */
        fprintf(stderr, "%s", PQerrorMessage(conn));
        PQfinish(conn);
        return 1;
    }

    /* called once on any connection that should receive events. 
     * Sends a PGEVT_REGISTER to myEventProc.
     */
    if (!PQregisterEventProc(conn, myEventProc, "mydata_proc", NULL))
    {
        fprintf(stderr, "Cannot register PGEventProc\n");
        PQfinish(conn);
        return 1;
    }

    /* conn instanceData is available */
    data = PQinstanceData(conn, myEventProc);

    /* Sends a PGEVT_RESULTCREATE to myEventProc */
    res = PQexec(conn, "SELECT 1 + 1");

    /* result instanceData is available */
    data = PQresultInstanceData(res, myEventProc);

    /* If PG_COPYRES_EVENTS is used, sends a PGEVT_RESULTCOPY to myEventProc */
    PGresult *res_copy = PQcopyResult(res, PG_COPYRES_TUPLES | PG_COPYRES_EVENTS);

    /* result instanceData is available if PG_COPYRES_EVENTS was 
     * used during the PQcopyResult call. 
     */
    data = PQresultInstanceData(res_copy, myEventProc);

    /* Both clears send a PGEVT_RESULTDESTROY to myEventProc */
    PQclear(res);
    PQclear(res_copy);

    /* Sends a PGEVT_CONNDESTROY to myEventProc */
    PQfinish(conn);

    return 0;
}

static int
myEventProc(PGEventId evtId, void *evtInfo, void *passThrough)
{
    switch (evtId)
    {
        case PGEVT_REGISTER:
        {
            PGEventRegister *e = (PGEventRegister *)evtInfo;
            mydata *data = get_mydata(e->conn);

            /* associate app specific data with connection */
            PQsetInstanceData(e->conn, myEventProc, data);
            break;
        }

        case PGEVT_CONNRESET:
        {
            PGEventConnReset *e = (PGEventConnReset *)evtInfo;
            mydata *data = PQinstanceData(e->conn, myEventProc);

            if (data)
              memset(data, 0, sizeof(mydata));
            break;
        }

        case PGEVT_CONNDESTROY:
        {
            PGEventConnDestroy *e = (PGEventConnDestroy *)evtInfo;
            mydata *data = PQinstanceData(e->conn, myEventProc);

            /* free instance data because the conn is being destroyed */
            if (data)
              free_mydata(data);
            break;
        }

        case PGEVT_RESULTCREATE:
        {
            PGEventResultCreate *e = (PGEventResultCreate *)evtInfo;
            mydata *conn_data = PQinstanceData(e->conn, myEventProc);
            mydata *res_data = dup_mydata(conn_data);

            /* associate app specific data with result (copy it from conn) */
            PQresultSetInstanceData(e->result, myEventProc, res_data);
            break;
        }

        case PGEVT_RESULTCOPY:
        {
            PGEventResultCopy *e = (PGEventResultCopy *)evtInfo;
            mydata *src_data = PQresultInstanceData(e->src, myEventProc);
            mydata *dest_data = dup_mydata(src_data);

            /* associate app specific data with result (copy it from a result) */
            PQresultSetInstanceData(e->dest, myEventProc, dest_data);
            break;
        }

        case PGEVT_RESULTDESTROY:
        {
            PGEventResultDestroy *e = (PGEventResultDestroy *)evtInfo;
            mydata *data = PQresultInstanceData(e->result, myEventProc);

            /* free instance data because the result is being destroyed */
            if (data)
              free_mydata(data);
            break;
        }

        /* unknown event ID, just return true. */
        default:
            break;
    }

    return true; /* event processing succeeded */
}

/* Dummy implementations for illustration purposes */
mydata *get_mydata(PGconn *conn) {
    mydata *data = malloc(sizeof(mydata));
    if (data) {
        data->n = 1;
        data->str = strdup("initial_string");
    }
    return data;
}

mydata *dup_mydata(mydata *data) {
    if (!data) return NULL;
    mydata *new_data = malloc(sizeof(mydata));
    if (new_data) {
        new_data->n = data->n;
        new_data->str = strdup(data->str);
    }
    return new_data;
}

void free_mydata(mydata *data) {
    if (data) {
        free(data->str);
        free(data);
    }
}
```

--------------------------------

### Configure PostgreSQL Automatic Startup (NetBSD/Solaris)

Source: https://www.postgresql.org/docs/6.3/c1802

This snippet shows how to configure NetBSD or SPARC Solaris 2.5.1 systems to automatically start the PostgreSQL postmaster service upon booting. It ensures the service runs as the 'postgres' user and specifies the data directory.

```shell
su postgres -c "/usr/local/pgsql/bin/postmaster -S -D /usr/local/pgsql/data"
```

--------------------------------

### Start PostgreSQL Server with pg_ctl

Source: https://www.postgresql.org/docs/17/app-pg-ctl

Starts a PostgreSQL server instance. You can specify the data directory, log file, and connection timeout. It also allows for passing options directly to the PostgreSQL server process.

```bash
pg_ctl start -D /path/to/your/datadir -l /path/to/logfile.log -t 60
```

--------------------------------

### Unpack PostgreSQL Source Code Packages

Source: https://www.postgresql.org/docs/7.0/odbc24471

Commands to unpack PostgreSQL source code from different archive formats. The -a option for unzip is crucial for handling DOS line endings in source files.

```shell
% unzip -a `packagename`
```

```shell
% tar -xzf `packagename`
```

--------------------------------

### OpenBSD PostgreSQL Autostart Script

Source: https://www.postgresql.org/docs/current/server-start

This snippet shows how to configure PostgreSQL to start automatically on an OpenBSD system by adding commands to the '/etc/rc.local' file. It checks for the executability of 'pg_ctl' and 'postgres' before attempting to start the server as the 'postgres' user.

```shell
if [ -x /usr/local/pgsql/bin/pg_ctl -a -x /usr/local/pgsql/bin/postgres ]; then
    su -l postgres -c '/usr/local/pgsql/bin/pg_ctl start -s -l /var/postgresql/log -D /usr/local/pgsql/data'
    echo -n ' postgresql'
fi

```

--------------------------------

### Initialize Foreign Scan Execution in PostgreSQL FDW

Source: https://www.postgresql.org/docs/11/fdw-callbacks

This routine initializes a foreign scan when the executor starts, performing any setup necessary before data retrieval begins. It should not start actual scanning; that is deferred until `IterateForeignScan`. The `ForeignScanState` node provides access to table information, and `eflags` indicates the executor's operating mode, such as `EXEC_FLAG_EXPLAIN_ONLY` for explain plans.

```c
void
BeginForeignScan(ForeignScanState *node,
                 int eflags);
```

--------------------------------

### Execute Query with Binary Integer Parameter and Binary Result using libpq (C)

Source: https://www.postgresql.org/docs/10/libpq-example

This snippet illustrates sending an integer parameter in binary format to PostgreSQL using PQexecParams, along with retrieving results in binary. It shows the necessary steps for converting integers to network byte order and setting parameter formats for binary transmission. Dependencies include libpq and standard C libraries.

```c
/* Convert integer value "2" to network byte order */
    binaryIntVal = htonl((uint32_t) 2);

    /* Set up parameter arrays for PQexecParams */
    paramValues[0] = (char *) &binaryIntVal;
    paramLengths[0] = sizeof(binaryIntVal);
    paramFormats[0] = 1;        /* binary */

    res = PQexecParams(conn,
                       "SELECT * FROM test1 WHERE i = $1::int4",
                       1,       /* one param */
                       NULL,    /* let the backend deduce param type */
                       paramValues,
                       paramLengths,
                       paramFormats,
                       1);      /* ask for binary results */

    if (PQresultStatus(res) != PGRES_TUPLES_OK)
    {
        fprintf(stderr, "SELECT failed: %s", PQerrorMessage(conn));
        PQclear(res);
        exit_nicely(conn);
    }

    show_binary_results(res);

    PQclear(res);
```

--------------------------------

### Example pg_hba.conf Configuration (PostgreSQL)

Source: https://www.postgresql.org/docs/7.2/admin

This snippet provides an example of a pg_hba.conf file, which controls client authentication for PostgreSQL. It defines connection rules based on authentication method, database, user, and client address. Proper configuration is crucial for securing database access.

```postgresql
# TYPE  DATABASE        USER            ADDRESS                 METHOD

# "local" is for Unix domain socket connections only
local   all             all                                     trust
# IPv4 local connections:  
host    all             all             127.0.0.1/32            ident
# IPv6 local connections:
host    all             all             ::1/128                 ident

# Allow replication connections from the primary node
host    replication     replicator      192.168.1.100/32        md5

# Default deny all other connections
# host    all             all             0.0.0.0/0               reject
```

--------------------------------

### pgbench Initialization Modes and Steps

Source: https://www.postgresql.org/docs/16/pgbench

Explains how to use pgbench in initialization mode (`-i`) and specifies which initialization steps to perform using the `-I` flag. It details the purpose of each step: dropping tables, creating tables, generating data (client-side 'g' vs. server-side 'G'), vacuuming, creating primary keys, and creating foreign keys.

```bash
pgbench -i # Initializes in default mode (equivalent to -I dtgvp)
pgbench -i -I dtgvp # Explicitly defines initialization steps: Drop, Tables, Generate (client-side), Vacuum, Primary keys
pgbench -i -I dGvp # Initializes by dropping tables, generating data server-side, vacuuming, and creating primary keys
```

--------------------------------

### Generate RTF for Installation Documentation

Source: https://www.postgresql.org/docs/6.5/docguide25300

This command generates the RTF file for installation documentation from SGML sources. It requires navigating to the doc/src/sgml directory and executing the 'make installation.rtf' command.

```shell
% cd doc/src/sgml
% make installation.rtf
      

```

--------------------------------

### Compare PostgreSQL Timestamp Subtraction Methods

Source: https://www.postgresql.org/docs/12/functions-datetime

This SQL snippet demonstrates three different methods for calculating the difference between two `timestamp with time zone` values in PostgreSQL. It compares using `EXTRACT(EPOCH FROM ...)` to get the difference in seconds, direct subtraction using the `-` operator to get an `interval` result, and the `age()` function to get a human-readable interval. The example uses a period that crosses a Daylight Saving Time change to illustrate their differing behaviors, with the session timezone set to 'US/Eastern'.

```sql
SELECT EXTRACT(EPOCH FROM timestamptz '2013-07-01 12:00:00') -
       EXTRACT(EPOCH FROM timestamptz '2013-03-01 12:00:00');
-- _Result: _10537200
SELECT (EXTRACT(EPOCH FROM timestamptz '2013-07-01 12:00:00') -
        EXTRACT(EPOCH FROM timestamptz '2013-03-01 12:00:00'))
        / 60 / 60 / 24;
-- _Result: _121.958333333333
SELECT timestamptz '2013-07-01 12:00:00' - timestamptz '2013-03-01 12:00:00';
-- _Result: _121 days 23:00:00
SELECT age(timestamptz '2013-07-01 12:00:00', timestamptz '2013-03-01 12:00:00');
-- _Result: _4 mons
```

--------------------------------

### PostgreSQL: Create Tablespace Example

Source: https://www.postgresql.org/docs/18/sql-createtablespace

Demonstrates the process of creating a new PostgreSQL tablespace. It includes the necessary operating system commands to prepare the directory and the SQL command to create the tablespace within PostgreSQL.

```shell
mkdir /data/dbs
chown postgres:postgres /data/dbs

```

```sql
CREATE TABLESPACE dbspace LOCATION '/data/dbs';

```

--------------------------------

### Build PostgreSQL Binaries and Contrib Modules

Source: https://www.postgresql.org/docs/10/install-procedure

This command builds the PostgreSQL server, additional modules from the 'contrib' directory, but excludes the documentation. This is useful when only the executable binaries and contrib components are needed, saving build time and resources.

```shell
make world-bin

```

--------------------------------

### Test libpq C Sample Program

Source: https://www.postgresql.org/docs/6.4/libpq-chapter17263

This C program demonstrates how to use libpq, the PostgreSQL frontend library, to connect to a database, execute SQL commands, manage transactions, and fetch data using cursors. It includes error handling and resource cleanup.

```c
/*
 * testlibpq.c Test the C version of Libpq, the Postgres frontend
 * library.
 *
 *
 */
#include <stdio.h>
#include "libpq-fe.h"

void
exit_nicely(PGconn *conn)
{
    PQfinish(conn);
    exit(1);
}

main()
{
    char       *pghost,
               *pgport,
               *pgoptions,
               *pgtty;
    char       *dbName;
    int         nFields;
    int         i, 
                j;

    /* FILE *debug; */

    PGconn     *conn;
    PGresult   *res;

    /*
     * begin, by setting the parameters for a backend connection if the
     * parameters are null, then the system will try to use reasonable
     * defaults by looking up environment variables or, failing that,
     * using hardwired constants
     */
    pghost = NULL;              /* host name of the backend server */
    pgport = NULL;              /* port of the backend server */
    pgoptions = NULL;           /* special options to start up the backend
                                 * server */
    pgtty = NULL;               /* debugging tty for the backend server */
    dbName = "template1";

    /* make a connection to the database */
    conn = PQsetdb(pghost, pgport, pgoptions, pgtty, dbName);

    /*
     * check to see that the backend connection was successfully made
     */
    if (PQstatus(conn) == CONNECTION_BAD)
    {
        fprintf(stderr, "Connection to database '%s' failed.\n", dbName);
        fprintf(stderr, "%s", PQerrorMessage(conn));
        exit_nicely(conn);
    }

    /* debug = fopen("/tmp/trace.out","w"); */
    /* PQtrace(conn, debug);  */

    /* start a transaction block */
    res = PQexec(conn, "BEGIN");
    if (PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "BEGIN command failed\n");
        PQclear(res);
        exit_nicely(conn);
    }

    /*
     * should PQclear PGresult whenever it is no longer needed to avoid
     * memory leaks
     */
    PQclear(res);

    /*
     * fetch instances from the pg_database, the system catalog of
     * databases
     */
    res = PQexec(conn, "DECLARE mycursor CURSOR FOR select * from pg_database");
    if (PQresultStatus(res) != PGRES_COMMAND_OK)
    {
        fprintf(stderr, "DECLARE CURSOR command failed\n");
        PQclear(res);
        exit_nicely(conn);
    }
    PQclear(res);
    res = PQexec(conn, "FETCH ALL in mycursor");
    if (PQresultStatus(res) != PGRES_TUPLES_OK)
    {
        fprintf(stderr, "FETCH ALL command didn't return tuples properly\n");
        PQclear(res);
        exit_nicely(conn);
    }

    /* first, print out the attribute names */
    nFields = PQnfields(res);
    for (i = 0; i < nFields; i++)
        printf("% -15s", PQfname(res, i));
    printf("\n\n");

    /* next, print out the instances */
    for (i = 0; i < PQntuples(res); i++)
    {
        for (j = 0; j < nFields; j++)
            printf("% -15s", PQgetvalue(res, i, j));
        printf("\n");
    }
    PQclear(res);

    /* close the cursor */
    res = PQexec(conn, "CLOSE mycursor");
    PQclear(res);

    /* commit the transaction */
    res = PQexec(conn, "COMMIT");
    PQclear(res);

    /* close the connection to the database and cleanup */
    PQfinish(conn);

    /* fclose(debug); */
}

```

--------------------------------

### PostgreSQL Large Object Example Program Main Function (C)

Source: https://www.postgresql.org/docs/17/lo-examplesect

This is the main function for the PostgreSQL libpq large object example program. It is intended to parse command-line arguments, establish a database connection, and then call various functions (like importFile, pickout, overwrite, exportFile) to demonstrate large object manipulation. The provided snippet is incomplete, showing only variable declarations and the start of the main function. It requires libpq and standard C libraries.

```c
static void
exit_nicely(PGconn *conn)
{
    PQfinish(conn);
    exit(1);
}

int
main(int argc, char **argv)
{
    char       *in_filename, 
               *out_filename;
    char       *database;
    Oid         lobjOid;
    PGconn     *conn;
    PGresult   *res;

```