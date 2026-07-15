### Solidity Relative Imports Examples

Source: https://docs.soliditylang.org/en/v0.8.30/path-resolution

Demonstrates relative import statements in Solidity, showing how paths are resolved relative to the importing file's location. These examples illustrate imports starting with './' and '../'.

```solidity
import "./util.sol" as util;    // source unit name: /project/lib/util.sol
import "../token.sol" as token; // source unit name: /project/token.sol

```

```solidity
import "./util.sol" as util;    // source unit name: lib/util.sol
import "../token.sol" as token; // source unit name: token.sol

```

```solidity
import "./util/./util.sol";         // source unit name: lib/src/../util/util.sol
import "./util//util.sol";          // source unit name: lib/src/../util/util.sol
import "../util/../array/util.sol"; // source unit name: lib/src/array/util.sol
import "../.././../util.sol";       // source unit name: util.sol
import "../../.././../util.sol";    // source unit name: util.sol

```

--------------------------------

### Solidity Binary Information (JSON)

Source: https://docs.soliditylang.org/en/v0.8.30/installing-solidity

Example of the `list.json` file format found in the solc-bin repository, detailing a specific compiler binary's metadata including path, version, build, hashes, and URLs.

```json
{
  "path": "solc-emscripten-wasm32-v0.7.4+commit.3f05b770.js",
  "version": "0.7.4",
  "build": "commit.3f05b770",
  "longVersion": "0.7.4+commit.3f05b770",
  "keccak256": "0x300330ecd127756b824aa13e843cb1f43c473cb22eaf3750d5fb9c99279af8c3",
  "sha256": "0x2b55ed5fec4d9625b6c7b3ab1abd2b7fb7dd2a9c68543bf0323db2c7e2d55af2",
  "urls": [
    "dweb:/ipfs/QmTLs5MuLEWXQkths41HiACoXDiH8zxyqBHGFDRSzVE5CS"
  ]
}

```

--------------------------------

### Install Solidity via Snap (Stable)

Source: https://docs.soliditylang.org/en/v0.8.30/installing-solidity

Installs the latest stable version of Solidity using the snap package manager.

```bash
sudo snap install solc
```

--------------------------------

### Install Solidity via Snap (Edge/Development)

Source: https://docs.soliditylang.org/en/v0.8.30/installing-solidity

Installs the development version of Solidity using the snap package manager with the --edge flag.

```bash
sudo snap install solc --edge
```

--------------------------------

### Install Solidity on Ubuntu (Nightly)

Source: https://docs.soliditylang.org/en/v0.8.30/installing-solidity

Installs the nightly build of the Solidity compiler on Ubuntu using PPAs.

```bash
sudo add-apt-repository ppa:ethereum/ethereum
sudo add-apt-repository ppa:ethereum/ethereum-dev
sudo apt-get update
sudo apt-get install solc
```

--------------------------------

### Install Solidity on Ubuntu (Stable)

Source: https://docs.soliditylang.org/en/v0.8.30/installing-solidity

Installs the latest stable version of the Solidity compiler on Ubuntu using PPA.

```bash
sudo add-apt-repository ppa:ethereum/ethereum
sudo apt-get update
sudo apt-get install solc
```

--------------------------------

### Solidity Contract Naming (CapWords)

Source: https://docs.soliditylang.org/en/v0.8.30/style-guide

Demonstrates the correct CapWords style for contract and library names, aligning them with their filenames. It also shows an example of importing and inheriting from another contract.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

// Owned.sol
contract Owned {
    address public owner;

    modifier onlyOwner {
        require(msg.sender == owner);
        _;
    }

    constructor() {
        owner = msg.sender;
    }

    function transferOwnership(address newOwner) public onlyOwner {
        owner = newOwner;
    }
}

```

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

import "./Owned.sol";


contract Congress is Owned, TokenRecipient {
    //...
}

```

--------------------------------

### Install Solidity from GitHub Commit Hash (Homebrew)

Source: https://docs.soliditylang.org/en/v0.8.30/installing-solidity

Installs a specific version of Solidity on macOS by checking out a commit hash from the Homebrew Ethereum repository and installing it.

```bash
git clone https://github.com/ethereum/homebrew-ethereum.git
cd homebrew-ethereum
git checkout <your-hash-goes-here>
brew unlink solidity
brew install solidity.rb
```

--------------------------------

### Clone Solidity Repository

Source: https://docs.soliditylang.org/en/v0.8.30/installing-solidity

Commands to clone the Solidity GitHub repository recursively and set up a personal fork as a second remote for development.

```bash
git clone --recursive https://github.com/ethereum/solidity.git
cd solidity
```

```bash
git remote add personal git@github.com:[username]/solidity.git
```

--------------------------------

### Solidity Simple Storage Contract with NatSpec Comments

Source: https://docs.soliditylang.org/en/v0.8.30/style-guide

An example of a basic Solidity smart contract demonstrating NatSpec comments for documenting functions, parameters, and return values. It includes state variables and functions to store and retrieve data.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

/// @author The Solidity Team
/// @title A simple storage example
contract SimpleStorage {
    uint storedData;

    /// Store `x`.
    /// @param x the new value to store
    /// @dev stores the number in the state variable `storedData`
    function set(uint x) public {
        storedData = x;
    }

    /// Return the stored value.
    /// @dev retrieves the value of the state variable `storedData`
    /// @return the stored value
    function get() public view returns (uint) {
        return storedData;
    }
}

```

--------------------------------

### Build Solidity with Build Script (Linux/macOS)

Source: https://docs.soliditylang.org/en/v0.8.30/installing-solidity

An easier method for Linux and macOS users to build Solidity by executing a provided build script. This script installs binaries like 'solc' and 'soltest' to '/usr/local/bin'.

```bash
#note: this will install binaries solc and soltest at usr/local/bin
./scripts/build.sh
```

--------------------------------

### Install Solidity Compiler via npm

Source: https://docs.soliditylang.org/en/v0.8.30/installing-solidity

Installs the `solcjs` command-line Solidity compiler globally using npm. Note that `solcjs` has fewer features than the full `solc` compiler and its command-line options are not compatible with `solc`.

```bash
npm install --global solc
```

--------------------------------

### Run Solidity Compiler via Docker (Help)

Source: https://docs.soliditylang.org/en/v0.8.30/installing-solidity

Pulls the latest stable Docker image for the Solidity compiler (`ethereum/solc:stable`) and runs it in a container to display help information. This is a way to access the compiler without local installation.

```bash
docker run ethereum/solc:stable --help
```

--------------------------------

### CMake Options Query

Source: https://docs.soliditylang.org/en/v0.8.30/installing-solidity

Command to list available CMake configuration options for the Solidity project. This helps in customizing the build process.

```bash
cmake .. -LH
```

--------------------------------

### Install Solidity on macOS using Homebrew

Source: https://docs.soliditylang.org/en/v0.8.30/installing-solidity

Installs the latest stable version of Solidity on macOS using Homebrew. This is a build-from-source version.

```bash
brew update
brew upgrade
brew tap ethereum/ethereum
brew install solidity
```

--------------------------------

### Install Dependencies Script

Source: https://docs.soliditylang.org/en/v0.8.30/installing-solidity

A PowerShell script to install external dependencies like 'boost' and 'cmake' for building Solidity. These dependencies are installed in the 'deps' subdirectory.

```powershell
scripts\install_deps.ps1
```

--------------------------------

### Long Function Declarations in Solidity

Source: https://docs.soliditylang.org/en/v0.8.30/style-guide

Provides examples of correctly formatted long function declarations in Solidity, with arguments, braces, and parentheses on separate lines.

```solidity
function thisFunctionHasLotsOfArguments(
    address a,
    address b,
    address c,
    address d,
    address e,
    address f
)
    public
{
    doSomething();
}
```

--------------------------------

### Solidity: Get Winner's Name

Source: https://docs.soliditylang.org/en/v0.8.30/solidity-by-example

Retrieves the name of the winning proposal by first determining the winning proposal's index using `winningProposal()` and then accessing its name from the proposals array.

```solidity
function winnerName() external view
            returns (bytes32 winnerName_) {
        winnerName_ = proposals[winningProposal()].name;
    }
```

--------------------------------

### Install Solidity on Arch Linux (AUR)

Source: https://docs.soliditylang.org/en/v0.8.30/installing-solidity

Installs Solidity using AUR packages for Arch Linux. Note: AUR packages are user-produced content.

```bash
yay -S solidity
# or for binary version
yay -S solidity-bin
```

--------------------------------

### Build Solidity for Windows with CMake

Source: https://docs.soliditylang.org/en/v0.8.30/installing-solidity

Command to build the Solidity project for Windows from the command line using CMake, specifying the 'Release' configuration.

```bash
cmake --build . --config Release
```

--------------------------------

### Solidity Compiler JSON Output Example

Source: https://docs.soliditylang.org/en/v0.8.30/using-the-compiler

This example demonstrates the typical JSON output from the Solidity compiler. It includes contract ABI, bytecode, and other metadata crucial for deploying and interacting with smart contracts.

```json
{
  "contracts": {
    "MyContract.sol": {
      "MyContract": {
        "abi": [
          {
            "inputs": [
              {
                "internalType": "uint256",
                "name": "_value",
                "type": "uint256"
              }
            ],
            "name": "setValue",
            "outputs": [],
            "stateMutability": "nonpayable",
            "type": "function"
          },
          {
            "inputs": [],
            "name": "value",
            "outputs": [
              {
                "internalType": "uint256",
                "name": "",
                "type": "uint256"
              }
            ],
            "stateMutability": "view",
            "type": "function"
          }
        ],
        "evm": {
          "bytecode": {
            "linkReferences": {},
            "object": "608060405234801561001057600080fd5b5060005050565b600080fdfe600081905091905056",
            "sourceMap": "64:7:0 64:25:0 85:9:0"
          },
          "deployedBytecode": {
            "immutableReferences": {},
            "object": "6080604052348015600f57600080fd5b50600050565b600081905091905056",
            "sourceMap": "64:7:0 64:25:0 85:9:0"
          },
          "methodIdentifiers": {
            "setValue(uint256)": "0x08585610"
          }
        }
      }
    }
  },
  "compiler": {
    "version": "0.8.19+commit.7f00f76b"
  },
  "sources": {},
  "evm": {},
  "bytecode": {},
  "linkReferences": {}
}

```

--------------------------------

### Solidity Compiler JSON Input Example

Source: https://docs.soliditylang.org/en/v0.8.30/using-the-compiler

This example illustrates the structure of a JSON input used to interact with the Solidity compiler. It specifies compilation settings like the compiler version, the source code, and optimization settings.

```json
{
  "language": "Solidity",
  "sources": {
    "MyContract.sol": {
      "content": "pragma solidity ^0.8.0;\ncontract MyContract {\n  uint256 public value;\n  function setValue(uint256 _value) public {\n    value = _value;\n  }\n}\n"
    }
  },
  "settings": {
    "optimizer": {
      "enabled": true,
      "runs": 200
    },
    "outputSelection": {
      "*": {
        "*": ["abi", "evm.bytecode", "evm.deployedBytecode", "evm.methodIdentifiers"]
      }
    }
  }
}

```

--------------------------------

### Install Specific Solidity Versions on macOS (Homebrew)

Source: https://docs.soliditylang.org/en/v0.8.30/installing-solidity

Installs older major versions of Solidity (e.g., 0.4.x, 0.5.x) on macOS using Homebrew.

```bash
brew install solidity@4
brew install solidity@5
```

--------------------------------

### Solidity Direct Import Examples

Source: https://docs.soliditylang.org/en/v0.8.30/path-resolution

Demonstrates various forms of direct imports in Solidity, including imports from project libraries, external packages, and URLs. These imports are resolved based on source unit names.

```solidity
import "/project/lib/util.sol";         // source unit name: /project/lib/util.sol
import "lib/util.sol";                  // source unit name: lib/util.sol
import "@openzeppelin/address.sol";     // source unit name: @openzeppelin/address.sol
import "https://example.com/token.sol"; // source unit name: https://example.com/token.sol

```

--------------------------------

### Solidity Operator Spacing - Correct Usage

Source: https://docs.soliditylang.org/en/v0.8.30/style-guide

Provides examples of correct operator spacing in Solidity, showing single spaces around operators for readability and optional exclusion of whitespace for higher-priority operators to denote precedence.

```solidity
x = 3;
x = 100 / 10;
x += 3 + 4;
x |= y && z;
x = 2**3 + 5;
x = 2*y + 3*z;
x = (a+b) * (a-b);
```

--------------------------------

### Solidity Library for Custom Types (BigInt)

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Illustrates using library internal functions and memory types to implement custom data types like 'bigint' without external call overhead. This example shows the start of a 'BigInt' library with a 'fromUint' function.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.0;

struct bigint {
    uint[] limbs;
}

library BigInt {
    function fromUint(uint x) internal pure returns (bigint memory r) {

```

--------------------------------

### Multiple Remappings for Different Versions

Source: https://docs.soliditylang.org/en/v0.8.30/path-resolution

Illustrates how to apply different remappings for the same module path, allowing the use of different versions of a library. This example redirects imports for 'github.com/ethereum/dapp-bin/' to 'dapp-bin/' for 'module1' and to 'dapp-bin_old/' for 'module2'.

```bash
solc module1:github.com/ethereum/dapp-bin/=dapp-bin/ \
     module2:github.com/ethereum/dapp-bin/=dapp-bin_old/ \
     --base-path /project \
     source.sol
```

--------------------------------

### Solidity Contract with Visibility Specifiers

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

This Solidity contract demonstrates the usage of `private`, `public`, and `internal` visibility specifiers for state variables and functions. It includes examples of setting and getting data, and internal computation.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract C {
    uint private data;

    function f(uint a) private pure returns(uint b) { return a + 1; }
    function setData(uint a) public { data = a; }
    function getData() public view returns(uint) { return data; }
    function compute(uint a, uint b) internal pure returns (uint) { return a + b; }
}

// This will not compile
contract D {
    function readData() public {
        C c = new C();
        uint local = c.f(7); // error: member `f` is not visible
        c.setData(3);
        local = c.getData();
        local = c.compute(3, 5); // error: member `compute` is not visible
    }
}

contract E is C {
    function g() public {
        C c = new C();
        uint val = compute(3, 5); // access to internal member (from derived to parent contract)
    }
}
```

--------------------------------

### Solidity Command Line Import Remapping

Source: https://docs.soliditylang.org/en/v0.8.30/path-resolution

Example of remapping a source unit name using the Solidity compiler command line. It shows how to map a project path to another path.

```shell
solc /project/=/contracts /project/contract.sol # source unit name: /project/contract.sol
```

--------------------------------

### Solidity Contract Example

Source: https://docs.soliditylang.org/en/v0.8.30/abi-spec

A sample Solidity contract demonstrating a constructor, an event, an error, and a function.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.4;


contract Test {
    constructor() { b = hex"12345678901234567890123456789012"; } 
    event Event(uint indexed a, bytes32 b);
    event Event2(uint indexed a, bytes32 b);
    error InsufficientBalance(uint256 available, uint256 required);
    function foo(uint a) public { emit Event(a, b); }
    bytes32 b;
}

```

--------------------------------

### Solidity String Quoting - Correct Usage

Source: https://docs.soliditylang.org/en/v0.8.30/style-guide

Illustrates the recommended practice of using double-quotes for strings in Solidity, including examples with embedded single quotes. This improves consistency and readability.

```solidity
str = "foo";
str = "Hamlet says, 'To be or not to be...'"
```

--------------------------------

### Import statement using remapping

Source: https://docs.soliditylang.org/en/v0.8.30/path-resolution

Shows a Solidity import statement that utilizes the remapping configured in the example. The import 'github.com/ethereum/dapp-bin/library/math.sol' is resolved by the compiler to 'dapp-bin/library/math.sol'.

```solidity
import "github.com/ethereum/dapp-bin/library/math.sol"; // source unit name: dapp-bin/library/math.sol
```

--------------------------------

### Solidity URL Import Remapping Example

Source: https://docs.soliditylang.org/en/v0.8.30/path-resolution

Illustrates remapping a URL-based import to a local directory using the Solidity compiler. It highlights the use of a leading colon for empty remapping contexts.

```shell
solc :https://github.com/ethereum/dapp-bin=/usr/local/dapp-bin contract.sol
```

--------------------------------

### Solidity Whitespace in Expressions

Source: https://docs.soliditylang.org/en/v0.8.30/style-guide

Provides examples of correct and incorrect whitespace usage within Solidity expressions. This includes spacing around parentheses, brackets, braces, commas, semicolons, and operators.

```solidity
spam(ham[1], Coin({name: "ham"}));

```

```solidity
function spam(uint i, Coin coin) public;

```

```solidity
x = 1;
y = 2;
longVariable = 3;

```

```solidity
receive() external payable {
    ...
}

fallback() external {
    ...
}

```

--------------------------------

### Build Solidity with CMake (Linux/macOS)

Source: https://docs.soliditylang.org/en/v0.8.30/installing-solidity

Steps to configure and build the Solidity project using CMake and Make on Linux and macOS systems. This process creates build artifacts in a 'build' directory.

```bash
mkdir build
cd build
cmake .. && make
```

--------------------------------

### Basic Import Remapping with Solc

Source: https://docs.soliditylang.org/en/v0.8.30/path-resolution

Demonstrates how to use solc with a basic import remapping to resolve imports from a cloned GitHub repository. It redirects imports starting with 'github.com/ethereum/dapp-bin/' to a local 'dapp-bin/' directory, using '/project' as the base path.

```bash
solc github.com/ethereum/dapp-bin/=dapp-bin/ --base-path /project source.sol
```

--------------------------------

### Whiskers Templating Syntax Examples

Source: https://docs.soliditylang.org/en/v0.8.30/contributing

Illustrates the syntax of the Whiskers templating system, including variable replacement, delimited areas, and conditional logic based on variable values.

```text
Any occurrence of `<name>` is replaced by the string-value of the supplied variable `name` without any escaping and without iterated replacements. An area can be delimited by `<#name>...</name>`. It is replaced by as many concatenations of its contents as there were sets of variables supplied to the template system, each time replacing any `<inner>` items by their respective value. Top-level variables can also be used inside such areas.
There are also conditionals of the form `<?name>...<!name>...</name>`, where template replacements continue recursively either in the first or the second segment depending on the value of the boolean parameter `name`. If `<?+name>...<!+name>...</+name>` is used, then the check is whether the string parameter `name` is non-empty.
```

--------------------------------

### Install GNU Coreutils on macOS with Homebrew

Source: https://docs.soliditylang.org/en/v0.8.30/contributing

This command installs GNU coreutils on macOS using the Homebrew package manager. This is often a prerequisite for certain testing scripts within the Solidity project that rely on GNU versions of standard utilities.

```shell
brew install coreutils
```

--------------------------------

### Contract C: BigInt Usage Example (Solidity)

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Demonstrates the usage of the BigInt library by creating BigInt instances, performing addition, and asserting a condition on the result.

```Solidity
contract C {
    using BigInt for bigint;

    function f() public pure {
        bigint memory x = BigInt.fromUint(7);
        bigint memory y = BigInt.fromUint(type(uint).max);
        bigint memory z = x.add(y);
        assert(z.limb(1) > 0);
    }
}
```

--------------------------------

### Short Function Declarations in Solidity

Source: https://docs.soliditylang.org/en/v0.8.30/style-guide

Demonstrates correct formatting for short function declarations in Solidity, emphasizing brace placement and indentation.

```solidity
function increment(uint x) public pure returns (uint) {
    return x + 1;
}

function increment(uint x) public pure onlyOwner returns (uint) {
    return x + 1;
}
```

--------------------------------

### Library Function Selector Example (Solidity)

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Shows how to obtain the function selector for a library function using the `.selector` member in Solidity.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.5.14 <0.9.0;

library L {
    function f(uint256) external {}
}

contract C {
    function g() public pure returns (bytes4) {
        return L.f.selector;
    }
}
```

--------------------------------

### Accept Xcode License on macOS

Source: https://docs.soliditylang.org/en/v0.8.30/installing-solidity

This command-line instruction is used on macOS to accept the Xcode license agreement, which is a prerequisite for command-line builds using Xcode's development tools.

```bash
sudo xcodebuild -license accept

```

--------------------------------

### Solidity Inheritance Example

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Demonstrates multiple inheritance, virtual functions, overriding, and calling base contract functions in Solidity. Includes contracts for ownership, event emission, configuration lookup, and name registration.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

contract Owned {
    address payable owner;
    constructor() { owner = payable(msg.sender); }
}

// Use `is` to derive from another contract. Derived
// contracts can access all non-private members including
// internal functions and state variables. These cannot be
// accessed externally via `this`, though.
contract Emittable is Owned {
    event Emitted();

    // The keyword `virtual` means that the function can change
    // its behavior in derived classes ("overriding").
    function emitEvent() virtual public {
        if (msg.sender == owner)
            emit Emitted();
    }
}

// These abstract contracts are only provided to make the
// interface known to the compiler. Note the function
// without body. If a contract does not implement all
// functions it can only be used as an interface.
abstract contract Config {
    function lookup(uint id) public virtual returns (address adr);
}

abstract contract NameReg {
    function register(bytes32 name) public virtual;
    function unregister() public virtual;
}

// Multiple inheritance is possible. Note that `Owned` is
// also a base class of `Emittable`, yet there is only a single
// instance of `Owned` (as for virtual inheritance in C++).
contract Named is Owned, Emittable {
    constructor(bytes32 name) {
        Config config = Config(0xD5f9D8D94886E70b06E474c3fB14Fd43E2f23970);
        NameReg(config.lookup(1)).register(name);
    }

    // Functions can be overridden by another function with the same name and
    // the same number/types of inputs. If the overriding function has different
    // types of output parameters, that causes an error.
    // Both local and message-based function calls take these overrides
    // into account.
    // If you want the function to override, you need to use the
    // `override` keyword. You need to specify the `virtual` keyword again
    // if you want this function to be overridden again.
    function emitEvent() public virtual override {
        if (msg.sender == owner) {
            Config config = Config(0xD5f9D8D94886E70b06E474c3fB14Fd43E2f23970);
            NameReg(config.lookup(1)).unregister();
            // It is still possible to call a specific
            // overridden function.
            Emittable.emitEvent();
        }
    }
}


// If a constructor takes an argument, it needs to be
// provided in the header or modifier-invocation-style at
// the constructor of the derived contract (see below).
contract PriceFeed is Owned, Emittable, Named("GoldFeed") {
    uint info;

    function updateInfo(uint newInfo) public {
        if (msg.sender == owner) info = newInfo;
    }

    // Here, we only specify `override` and not `virtual`.
    // This means that contracts deriving from `PriceFeed`
    // cannot change the behavior of `emitEvent` anymore.
    function emitEvent() public override(Emittable, Named) { Named.emitEvent(); }
    function get() public view returns(uint r) { return info; }
}

```

--------------------------------

### Compile Solidity File using Docker

Source: https://docs.soliditylang.org/en/v0.8.30/installing-solidity

Compiles a Solidity file (`Contract.sol`) using the stable Docker image. It mounts a local directory for input and output, and specifies compilation flags like `--abi`, `--bin`, and `--output-dir`.

```bash
docker run \
    --volume "/tmp/some/local/path/:/sources/" \
    ethereum/solc:stable \
        /sources/Contract.sol \
        --abi \
        --bin \
        --output-dir /sources/output/
```

--------------------------------

### Yul Data Size and Offset (datasize, dataoffset)

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Yul functions to get the size and starting byte offset of string literals within the data section of a Yul object. These are typically used for accessing contract metadata or other static data.

```Yul
datasize("myString");
dataoffset("myString");
```

--------------------------------

### Solidity Function Parameters Example

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Shows how to declare function parameters in Solidity, similar to variable declarations. Unused parameter names can be omitted. The example demonstrates a function that accepts two uint parameters and assigns their sum to a state variable.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract Simple {
    uint sum;
    function taker(uint a, uint b) public {
        sum = a + b;
    }
}

```

--------------------------------

### Solidity Modulo Operation Examples

Source: https://docs.soliditylang.org/en/v0.8.30/types

Illustrates the behavior of the modulo operator in Solidity, showing that the result takes the sign of the left operand. Includes examples with positive and negative operands.

```solidity
int256(5) % int256(2) == int256(1)
int256(5) % int256(-2) == int256(1)
int256(-5) % int256(2) == int256(-1)
int256(-5) % int256(-2) == int256(-1)
```

--------------------------------

### Source Mapping Compression Example

Source: https://docs.soliditylang.org/en/v0.8.30/internals/source_mappings

Illustrates the compression rules applied to source mappings for bytecode, showing how omitted fields inherit values from preceding elements.

```text
The following source mappings represent the same information:
`1:2:1;1:9:1;2:1:2;2:1:2;2:1:2`
`1:2:1;:9;2:1:2;;`
```

--------------------------------

### Configure Solidity Build with CMake (Windows)

Source: https://docs.soliditylang.org/en/v0.8.30/installing-solidity

Command to configure the Solidity build using CMake on Windows, specifically targeting the Visual Studio 2019 generator. This creates a 'solidity.sln' file.

```bash
mkdir build
cd build
cmake -G "Visual Studio 16 2019" ..
```

--------------------------------

### Compile Solidity using Docker with Standard JSON Interface

Source: https://docs.soliditylang.org/en/v0.8.30/installing-solidity

Compiles Solidity code using the standard JSON interface with a Docker image. It redirects input from `input.json` and output to `output.json`. This method is recommended for tool integration and does not require mounting directories if the JSON input is self-contained.

```bash
docker run ethereum/solc:stable --standard-json < input.json > output.json
```

--------------------------------

### SSATransform Example - Solidity

Source: https://docs.soliditylang.org/en/v0.8.30/internals/optimizer

Demonstrates the transformation of repeated variable assignments in Solidity using the SSATransform stage. It shows how 'a := 3' is converted to 'let a_3 := 3; a := a_3'.

```Solidity
{
    let a := 1
    mstore(a, 2)
    a := 3
}
```

```Solidity
{
    let a_1 := 1
    let a := a_1
    mstore(a_1, 2)
    let a_3 := 3
    a := a_3
}
```

--------------------------------

### Solidity: Event Definition and Emitter Formatting

Source: https://docs.soliditylang.org/en/v0.8.30/style-guide

Demonstrates the correct formatting for long event definitions and event emitters in Solidity, with each argument on a new line.

```Solidity
event LongAndLotsOfArgs(
    address sender,
    address recipient,
    uint256 publicKey,
    uint256 amount,
    bytes32[] options
);

emit LongAndLotsOfArgs(
    sender,
    recipient,
    publicKey,
    amount,
    options
);

```

--------------------------------

### Multiline Return Statements in Solidity

Source: https://docs.soliditylang.org/en/v0.8.30/style-guide

Demonstrates the correct formatting for multiline return statements and output parameters in long Solidity function declarations.

```solidity
function thisFunctionNameIsReallyLong(
    address a,
    address b,
    address c
)
    public
    returns (
        address someAddressName,
        uint256 LongArgument,
        uint256 Argument
    )
{
    doSomething()

    return (
        veryLongReturnArg1,
        veryLongReturnArg2,
        veryLongReturnArg3
    );
}
```

--------------------------------

### Solidity Constant and Immutable State Variables Example

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Demonstrates the declaration and usage of constant and immutable state variables in Solidity. Constant variables are assigned at compile-time, while immutable variables can be assigned at construction time. The example shows their initialization, usage in functions, and the ability to access environment data for immutable assignments during construction.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.21;

uint constant X = 32**22 + 8;

contract C {
    string constant TEXT = "abc";
    bytes32 constant MY_HASH = keccak256("abc");
    uint immutable decimals = 18;
    uint immutable maxBalance;
    address immutable owner = msg.sender;

    constructor(uint decimals_, address ref) {
        if (decimals_ != 0)
            // Immutables are only immutable when deployed.
            // At construction time they can be assigned to any number of times.
            decimals = decimals_;

        // Assignments to immutables can even access the environment.
        maxBalance = ref.balance;
    }

    function isBalanceTooHigh(address other) public view returns (bool) {
        return other.balance > maxBalance;
    }
}

```

--------------------------------

### Solidity: Single-line and Multi-line Comments

Source: https://docs.soliditylang.org/en/v0.8.30/layout-of-source-files

Demonstrates the usage of single-line comments starting with '//' and multi-line comments enclosed in '/* ... */' in Solidity.

```Solidity
// This is a single-line comment.

/*
This is a
multi-line comment.
*/
```

--------------------------------

### Yul Code for Keccak-256 Calculation

Source: https://docs.soliditylang.org/en/v0.8.30/internals/optimizer

This Yul code snippet demonstrates the equivalent functionality to the Solidity assembly example, using calldataload, mstore, and keccak256 to compute a hash.

```yul
let x := calldataload(0)
mstore(x, 100)
let value := keccak256(x, 32)

```

--------------------------------

### Solidity String and Bytes Concatenation Example

Source: https://docs.soliditylang.org/en/v0.8.30/types

Demonstrates the usage of `string.concat` and `bytes.concat` functions in Solidity. It shows how to concatenate strings and byte arrays, including type conversions and length assertions. The example highlights the differences in handling various data types when concatenating.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.12;

contract C {
    string s = "Storage";
    function f(bytes calldata bc, string memory sm, bytes16 b) public view {
        string memory concatString = string.concat(s, string(bc), "Literal", sm);
        assert((bytes(s).length + bc.length + 7 + bytes(sm).length) == bytes(concatString).length);

        bytes memory concatBytes = bytes.concat(bytes(s), bc, bc[:2], "Literal", bytes(sm), b);
        assert((bytes(s).length + bc.length + 2 + 7 + bytes(sm).length + b.length) == concatBytes.length);
    }
}

```

--------------------------------

### Solidity Yul: For-Loop for Iteration with Step

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Shows a standard for-loop in Yul, including initialization, a condition, and a post-iteration step. This example iterates, loading and summing values from memory.

```Solidity Yul
{
    let x := 0
    for { let i := 0 } lt(i, 0x100) { i := add(i, 0x20) } {
        x := add(x, mload(i))
    }
}

```

--------------------------------

### Solidity Contract Example

Source: https://docs.soliditylang.org/en/v0.8.30/analysing-compilation-output

A simple Solidity contract demonstrating a pure function that returns the value 1. This serves as a basis for analyzing compiler output.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.5.0 <0.9.0;
contract C {
    function one() public pure returns (uint) {
        return 1;
    }
}

```

--------------------------------

### Solidity Mapping Syntax - Correct Usage

Source: https://docs.soliditylang.org/en/v0.8.30/style-guide

Shows the correct way to declare mappings in Solidity, emphasizing no space between the 'mapping' keyword and its type, and no whitespace within nested mappings. This adheres to the style guide for clarity.

```solidity
mapping(uint => uint) map;
mapping(address => bool) registeredAddresses;
mapping(uint => mapping(bool => Data[])) public data;
mapping(uint => mapping(uint => s)) data;
```

--------------------------------

### Get Contract Code using Inline Assembly in Solidity

Source: https://docs.soliditylang.org/en/v0.8.30/assembly

This snippet demonstrates how to retrieve the bytecode of another contract using inline assembly in Solidity. It calculates the code size, allocates memory for the output, and uses `extcodecopy` to copy the contract's code. This is an example of enhancing Solidity's capabilities with reusable assembly libraries.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

library GetCode {
    function at(address addr) public view returns (bytes memory code) {
        assembly {
            // retrieve the size of the code, this needs assembly
            let size := extcodesize(addr)
            // allocate output byte array - this could also be done without assembly
            // by using code = new bytes(size)
            code := mload(0x40)
            // new "memory end" including padding
            mstore(0x40, add(code, and(add(add(size, 0x20), 0x1f), not(0x1f))))
            // store length in memory
            mstore(code, size)
            // actually retrieve the code, this needs assembly
            extcodecopy(addr, add(code, 0x20), 0, size)
        }
    }
}
```

--------------------------------

### Solidity Struct Memory Layout Example

Source: https://docs.soliditylang.org/en/v0.8.30/internals/layout_in_memory

Illustrates the memory occupation of a Solidity struct. The example struct S, containing two uints and two uint8s, takes up 128 bytes in memory.

```solidity
struct S {
    uint a;
    uint b;
    uint8 c;
    uint8 d;
}

```

--------------------------------

### Solidity Compiler File Loading with --allow-paths

Source: https://docs.soliditylang.org/en/v0.8.30/path-resolution

Demonstrates how to invoke the Solidity compiler with specific input files, remappings, base paths, include paths, and a list of allowed paths for importing.

```shell
cd /home/user/project/
solc token/contract.sol \
    lib/util.sol=libs/util.sol \
    --base-path=token/ \
    --include-path=/lib/ \
    --allow-paths=../utils/,/tmp/libraries

```

--------------------------------

### Solidity Contract Example: Mappings and Structs

Source: https://docs.soliditylang.org/en/v0.8.30/internals/layout_in_storage

Demonstrates a Solidity contract with a struct and nested mappings, illustrating the storage layout rules discussed. This example helps visualize how complex data structures are stored in the contract's state.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;


contract C {
    struct S { uint16 a; uint16 b; uint256 c; }
    uint x;
    mapping(uint => mapping(uint => S)) data;
}

```

--------------------------------

### Unchecked Loop Increment - Eligible Loop Example

Source: https://docs.soliditylang.org/en/v0.8.30/internals/optimizer

Example of a 'for' loop eligible for the unchecked increment optimization. The counter `i` is local, not modified in the body, and incremented with `++i`.

```Solidity
for (uint i = X; i < Y; ++i) {
    // variable i is not modified in the loop body
}
```

--------------------------------

### Solidity Array Variable Declaration - Correct Usage

Source: https://docs.soliditylang.org/en/v0.8.30/style-guide

Demonstrates the correct syntax for declaring array variables in Solidity, showing no space between the type and the brackets. This ensures adherence to the style guide.

```solidity
uint[] x;
```

--------------------------------

### Solidity Compiler Command with Base and Include Paths

Source: https://docs.soliditylang.org/en/v0.8.30/path-resolution

This command demonstrates how to compile a Solidity contract while specifying the base path and additional include paths. It's useful for projects that depend on external libraries managed by package managers like npm.

```bash
solc contract.sol \
    --base-path . \
    --include-path node_modules/ \
    --include-path /usr/local/lib/node_modules/
```

--------------------------------

### Solidity SimplePaymentChannel Contract

Source: https://docs.soliditylang.org/en/v0.8.30/solidity-by-example

The main contract for a simple payment channel, managing sender, recipient, expiration, and payment logic. It inherits from Frozeable for state management.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

contract Frozeable {
    bool private _frozen = false;

    modifier notFrozen() {
        require(!_frozen, "Inactive Contract.");
        _;
    }

    function freeze() internal {
        _frozen = true;
    }
}

contract SimplePaymentChannel is Frozeable {
    address payable public sender;    // The account sending payments.
    address payable public recipient; // The account receiving the payments.
    uint256 public expiration;        // Timeout in case the recipient never closes.

    constructor (address payable recipientAddress, uint256 duration)
        payable
    {
        sender = payable(msg.sender);
        recipient = recipientAddress;
        expiration = block.timestamp + duration;
    }

    /// the recipient can close the channel at any time by presenting a
    /// signed amount from the sender. the recipient will be sent that amount,
    /// and the remainder will go back to the sender
    function close(uint256 amount, bytes memory signature)
        external
        notFrozen
    {
        require(msg.sender == recipient);
        require(isValidSignature(amount, signature));

        recipient.transfer(amount);
        freeze();
        sender.transfer(address(this).balance);
    }

    /// the sender can extend the expiration at any time
    function extend(uint256 newExpiration)
        external
        notFrozen
    {
        require(msg.sender == sender);
        require(newExpiration > expiration);

        expiration = newExpiration;
    }

    /// if the timeout is reached without the recipient closing the channel,
    /// then the Ether is released back to the sender.
    function claimTimeout() 
        external
        notFrozen
    {
        require(block.timestamp >= expiration);
        freeze();
        sender.transfer(address(this).balance);
    }

    function isValidSignature(uint256 amount, bytes memory signature)
        internal
        view
        returns (bool)
    {
        bytes32 message = prefixed(keccak256(abi.encodePacked(this, amount)));
        // check that the signature is from the payment sender
        return recoverSigner(message, signature) == sender;
    }

    /// All functions below this are just taken from the chapter
    /// 'creating and verifying signatures' chapter.
    function splitSignature(bytes memory sig)
        internal
        pure
        returns (uint8 v, bytes32 r, bytes32 s)
    {
        require(sig.length == 65);

        assembly {
            // first 32 bytes, after the length prefix
            r := mload(add(sig, 32))
            // second 32 bytes
            s := mload(add(sig, 64))
            // final byte (first byte of the next 32 bytes)
            v := byte(0, mload(add(sig, 96)))
        }
        return (v, r, s);
    }

    function recoverSigner(bytes32 message, bytes memory sig)
        internal
        pure
        returns (address)
    {
        (uint8 v, bytes32 r, bytes32 s) = splitSignature(sig);
        return ecrecover(message, v, r, s);
    }

    /// builds a prefixed hash to mimic the behavior of eth_sign.
    function prefixed(bytes32 hash) internal pure returns (bytes32) {
        return keccak256(abi.encodePacked("\x19Ethereum Signed Message:\n32", hash));
    }
}

```

--------------------------------

### Solidity NatSpec Example with Dynamic Expressions

Source: https://docs.soliditylang.org/en/v0.8.30/natspec-format

An example of a Solidity NatSpec comment that includes a dynamic expression. The compiler can process these expressions to provide more context-aware documentation to end-users based on runtime values.

```solidity
/// @notice This function will multiply `a` by 7

```

--------------------------------

### Solidity Import Statements Placement

Source: https://docs.soliditylang.org/en/v0.8.30/style-guide

Illustrates the correct placement of import statements at the top of a Solidity file. Imports should precede contract definitions. This ensures all necessary contracts and libraries are available before they are referenced.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

import "./Owned.sol";

contract A {
    // ...
}


contract B is Owned {
    // ...
}

```

--------------------------------

### Pseudo-SSA Transformation Example

Source: https://docs.soliditylang.org/en/v0.8.30/internals/optimizer

Demonstrates the transformation of a Solidity code snippet into a pseudo-SSA form. This process makes variables more distinct based on control flow changes, aiding subsequent optimizations.

```solidity
{
    let a := calldataload(0)
    let b := calldataload(0x20)
    if gt(a, 0) {
        b := mul(b, 0x20)
    }
    a := add(a, 1)
    sstore(a, add(b, 0x20))
}
```

```solidity
{
    let _1 := 0
    let a_9 := calldataload(_1)
    let a := a_9
    let _2 := 0x20
    let b_10 := calldataload(_2)
    let b := b_10
    let _3 := 0
    let _4 := gt(a_9, _3)
    if _4
    {
        let _5 := 0x20
        let b_11 := mul(b_10, _5)
        b := b_11
    }
    let b_12 := b
    let _6 := 1
    let a_13 := add(a_9, _6)
    let _7 := 0x20
    let _8 := add(b_12, _7)
    sstore(a_13, _8)
}
```

--------------------------------

### Yul Code with Memory Tracking for Keccak-256

Source: https://docs.soliditylang.org/en/v0.8.30/internals/optimizer

This Yul example illustrates how the optimizer tracks memory locations. It shows an mstore operation and a subsequent keccak256 hash calculation, highlighting the condition under which the hash can be evaluated at compile time.

```yul
let x := calldataload(0)
mstore(x, 100)
// Current knowledge memory location x -> 100
let y := add(x, 32)
// Does not clear the knowledge that x -> 100, since y does not write to [x, x + 32)
mstore(y, 200)
// This Keccak-256 can now be evaluated
let value := keccak256(x, 32)

```

--------------------------------

### Sign Message with Web3.js (Hashing First)

Source: https://docs.soliditylang.org/en/v0.8.30/solidity-by-example

This snippet demonstrates how to sign a message using web3.js by first hashing the message. The `web3.utils.sha3` function is used for hashing, and then `web3.eth.personal.sign` is used to sign the hash with the default account. Note that `personal.sign` prepends the message length, which is consistent when hashing first.

```javascript
/// Hashing first makes things easier
var hash = web3.utils.sha3("message to sign");
web3.eth.personal.sign(hash, web3.eth.defaultAccount, function () { console.log("Signed"); });
```

--------------------------------

### Solidity: Prefixed Message Hashing

Source: https://docs.soliditylang.org/en/v0.8.30/solidity-by-example

This function creates a prefixed hash of a given message hash, mimicking the behavior of `eth_sign`. It prepends a standard prefix to the message before hashing it with Keccak-256, ensuring compatibility with off-chain signing methods.

```Solidity
function prefixed(bytes32 hash) internal pure returns (bytes32) {
    return keccak256(abi.encodePacked("\x19Ethereum Signed Message:\n32", hash));
}
```

--------------------------------

### Solidity Stateful Library Example (Set)

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Demonstrates a Solidity library 'Set' that manages a mapping to store unique uint values. It includes functions to insert, remove, and check for the existence of values, interacting with a 'Data' struct passed as a storage reference.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;


// We define a new struct datatype that will be used to
// hold its data in the calling contract.
struct Data {
    mapping(uint => bool) flags;
}

library Set {
    // Note that the first parameter is of type "storage
    // reference" and thus only its storage address and not
    // its contents is passed as part of the call.  This is a
    // special feature of library functions.  It is idiomatic
    // to call the first parameter `self`, if the function can
    // be seen as a method of that object.
    function insert(Data storage self, uint value)
        public
        returns (bool)
    {
        if (self.flags[value])
            return false; // already there
        self.flags[value] = true;
        return true;
    }

    function remove(Data storage self, uint value)
        public
        returns (bool)
    {
        if (!self.flags[value])
            return false; // not there
        self.flags[value] = false;
        return true;
    }

    function contains(Data storage self, uint value)
        public
        view
        returns (bool)
    {
        return self.flags[value];
    }
}


contract C {
    Data knownValues;

    function register(uint value) public {
        // The library functions can be called without a
        // specific instance of the library, since the
        // "instance" will be the current contract.
        require(Set.insert(knownValues, value));
    }
    // In this contract, we can also directly access knownValues.flags, if we want.
}

```

--------------------------------

### Solidity Free Function Example

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Illustrates the use of a free function ('sum') defined outside a contract, which is implicitly internal. Its code is included in contracts that call it, behaving like internal library functions. The example shows how a contract can call this free function.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.1 <0.9.0;

function sum(uint[] memory arr) pure returns (uint s) {
    for (uint i = 0; i < arr.length; i++)
        s += arr[i];
}

contract ArrayExample {
    bool found;
    function f(uint[] memory arr) public {
        // This calls the free function internally.
        // The compiler will add its code to the contract.
        uint s = sum(arr);
        require(s >= 10);
        found = true;
    }
}

```

--------------------------------

### JavaScript: Verify Payment Signatures using ethereumjs-util

Source: https://docs.soliditylang.org/en/v0.8.30/solidity-by-example

This JavaScript code demonstrates how to verify signatures for payment channels using the ethereumjs-util library. It includes functions for prefixing hashes, recovering the signer's address from a signature, and validating the signature against an expected signer.

```javascript
function prefixed(hash) {
    return ethereumjs.ABI.soliditySHA3(
        ["string", "bytes32"],
        ["\x19Ethereum Signed Message:\n32", hash]
    );
}

function recoverSigner(message, signature) {
    var split = ethereumjs.Util.fromRpcSig(signature);
    var publicKey = ethereumjs.Util.ecrecover(message, split.v, split.r, split.s);
    var signer = ethereumjs.Util.pubToAddress(publicKey).toString("hex");
    return signer;
}

function isValidSignature(contractAddress, amount, signature, expectedSigner) {
    var message = prefixed(constructPaymentMessage(contractAddress, amount));
    var signer = recoverSigner(message, signature);
    return signer.toLowerCase() ==
        ethereumjs.Util.stripHexPrefix(expectedSigner).toLowerCase();
}
```

--------------------------------

### Solidity: OwnedToken Contract Example

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

An example Solidity contract named `OwnedToken` that stores owner, name, and creator information. It includes a constructor to initialize these fields and functions to change the name and transfer ownership, with access control based on the contract's creator and owner.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.22 <0.9.0;


contract OwnedToken {
    // `TokenCreator` is a contract type that is defined below.
    // It is fine to reference it as long as it is not used
    // to create a new contract.
    TokenCreator creator;
    address owner;
    bytes32 name;

    // This is the constructor which registers the
    // creator and the assigned name.
    constructor(bytes32 name_) {
        // State variables are accessed via their name
        // and not via e.g. `this.owner`. Functions can
        // be accessed directly or through `this.f`,
        // but the latter provides an external view
        // to the function. Especially in the constructor,
        // you should not access functions externally,
        // because the function does not exist yet.
        // See the next section for details.
        owner = msg.sender;

        // We perform an explicit type conversion from `address`
        // to `TokenCreator` and assume that the type of
        // the calling contract is `TokenCreator`, there is
        // no real way to verify that.
        // This does not create a new contract.
        creator = TokenCreator(msg.sender);
        name = name_;
    }

    function changeName(bytes32 newName) public {
        // Only the creator can alter the name.
        // We compare the contract based on its
        // address which can be retrieved by
        // explicit conversion to address.
        if (msg.sender == address(creator))
            name = newName;
    }

    function transfer(address newOwner) public {
        // Only the current owner can transfer the token.
        if (msg.sender != owner) return;

        // We ask the creator contract if the transfer
        // should proceed by using a function of the
        // `TokenCreator` contract defined below. If
        // the call fails (e.g. due to out-of-gas),
        // the execution also fails here.
        if (creator.isTokenTransferOK(owner, newOwner))
            owner = newOwner;
    }
}

```

--------------------------------

### Set EVM Version via solc Command-Line

Source: https://docs.soliditylang.org/en/v0.8.30/using-the-compiler

Provides an example of how to specify the target Ethereum Virtual Machine (EVM) version when compiling Solidity code using the solc command-line interface.

```shell
solc --evm-version <VERSION> contract.sol
```

--------------------------------

### Inherited Constructor Formatting in Solidity

Source: https://docs.soliditylang.org/en/v0.8.30/style-guide

Illustrates formatting for inherited constructor functions in Solidity when base contracts require arguments, placing them on new lines for readability.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;
// Base contracts just to make this compile
contract B {
    constructor(uint) {
    }
}


contract C {
    constructor(uint, uint) {
    }
}


contract D {
    constructor(uint) {
    }
}
```

--------------------------------

### Solidity: Long Assignment Formatting

Source: https://docs.soliditylang.org/en/v0.8.30/style-guide

Provides guidance on formatting long assignment statements in Solidity, ensuring readability by placing arguments on separate lines.

```Solidity
thisIsALongNestedMapping[being][set][toSomeValue] = someFunction(
    argument1,
    argument2,
    argument3,
    argument4
);

```

--------------------------------

### Skip Semantic Tests

Source: https://docs.soliditylang.org/en/v0.8.30/contributing

Disables semantic tests if the `evmone` library is not installed or accessible. The `evmone` library is required for semantic and gas tests.

```shell
scripts/soltest.sh --no-semantic-tests
```

--------------------------------

### Solidity: Token Contract with Modular Balance Handling

Source: https://docs.soliditylang.org/en/v0.8.30/solidity-by-example

A Solidity smart contract implementing a basic token with transfer and approval functionalities. It utilizes a modular approach by employing an external library 'Balances' for handling internal balance transfers, ensuring integrity and reducing complexity.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.5.0 <0.9.0;

library Balances {
    function move(mapping(address => uint256) storage balances, address from, address to, uint amount) internal {
        require(balances[from] >= amount);
        require(balances[to] + amount >= balances[to]);
        balances[from] -= amount;
        balances[to] += amount;
    }
}

contract Token {
    mapping(address => uint256) balances;
    using Balances for *;
    mapping(address => mapping(address => uint256)) allowed;

    event Transfer(address from, address to, uint amount);
    event Approval(address owner, address spender, uint amount);

    function transfer(address to, uint amount) external returns (bool success) {
        balances.move(msg.sender, to, amount);
        emit Transfer(msg.sender, to, amount);
        return true;

    }

    function transferFrom(address from, address to, uint amount) external returns (bool success) {
        require(allowed[from][msg.sender] >= amount);
        allowed[from][msg.sender] -= amount;
        balances.move(from, to, amount);
        emit Transfer(from, to, amount);
        return true;
    }

    function approve(address spender, uint tokens) external returns (bool success) {
        require(allowed[msg.sender][spender] == 0, "");
        allowed[msg.sender][spender] = tokens;
        emit Approval(msg.sender, spender, tokens);
        return true;
    }

    function balanceOf(address tokenOwner) external view returns (uint balance) {
        return balances[tokenOwner];
    }

}
```

--------------------------------

### AST Source Mapping Notation

Source: https://docs.soliditylang.org/en/v0.8.30/internals/source_mappings

Explains the notation used for source mappings within the Abstract Syntax Tree (AST). It specifies the byte-offset to the start, length in bytes, and source file index.

```text
`s:l:f`
Where `s` is the byte-offset to the start of the range in the source file, `l` is the length of the source range in bytes and `f` is the source index.
```

--------------------------------

### Solidity: Contract Spacing

Source: https://docs.soliditylang.org/en/v0.8.30/style-guide

Demonstrates correct spacing between top-level contract declarations in Solidity. Two blank lines are required between contracts.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

contract A {
    // ...
}


contract B {
    // ...
}


contract C {
    // ...
}

```

--------------------------------

### Solidity: Checked and Unchecked Arithmetic Example

Source: https://docs.soliditylang.org/en/v0.8.30/control-structures

Demonstrates the difference between default checked arithmetic (reverts on overflow/underflow) and unchecked arithmetic (wraps on overflow/underflow) in Solidity.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.0;
contract C {
    function f(uint a, uint b) pure public returns (uint) {
        // This subtraction will wrap on underflow.
        unchecked { return a - b; }
    }
    function g(uint a, uint b) pure public returns (uint) {
        // This subtraction will revert on underflow.
        return a - b;
    }
}

```

--------------------------------

### Compile Solidity Files via CLI

Source: https://docs.soliditylang.org/en/v0.8.30/path-resolution

Compiles specified Solidity files using the solc command-line interface. Input paths are converted to canonical forms for source unit naming.

```shell
solc contract.sol /usr/local/dapp-bin/token.sol

```

--------------------------------

### Solidity CLI Path Normalization Example

Source: https://docs.soliditylang.org/en/v0.8.30/path-resolution

Illustrates a scenario where the Solidity compiler might issue an error due to non-unique relative paths after stripping. This occurs when multiple source files with the same name exist under different base or include paths.

```shell
solc /project/contract.sol --base-path /project --include-path /lib
```

--------------------------------

### Solidity Contract Declaration

Source: https://docs.soliditylang.org/en/v0.8.30/contributing

Demonstrates the basic structure of a Solidity contract, including the pragma directive for version specification and the contract keyword. It's essential for all Solidity code examples.

```solidity
pragma solidity >=0.4.0 <0.9.0;

contract SimpleContract {
    // Contract content here
}
```

--------------------------------

### Solidity Compiler Basic Usage

Source: https://docs.soliditylang.org/en/v0.8.30/using-the-compiler

Demonstrates basic usage of the Solidity command-line compiler (solc) for compiling a single source file and generating various output formats. It explains how to print the binary, abstract syntax tree, and assembly.

```bash
solc --help
solc --bin sourceFile.sol
solc -o outputDirectory --bin --ast-compact-json --asm sourceFile.sol
```

--------------------------------

### Solidity Inlining Example

Source: https://docs.soliditylang.org/en/v0.8.30/internals/optimizer

Demonstrates how the Solidity optimizer can inline simple internal functions. It shows the transformation from a sequence with a jump into a function to an inlined version, eventually removing the function definition if unused.

```assembly
  tag_return
  tag_f
  jump      // in
tag_return:
  ...opcodes after call to f...

tag_f:
  ...body of function f...
  jump      // out

```

```assembly
  tag_return
  ...body of function f...
  jump
tag_return:
  ...opcodes after call to f...

tag_f:
  ...body of function f...
  jump      // out

```

```assembly
  ...body of function f...
  tag_return
  jump
tag_return:
  ...opcodes after call to f...

```

```assembly
...body of function f...
...opcodes after call to f...

```

--------------------------------

### Solidity Yul: For-Loop as a While-Loop

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Demonstrates using a for-loop in Yul as a while-loop by leaving the initialization and post-iteration parts empty. This example sums values from memory while a condition is met.

```Solidity Yul
{
    let x := 0
    let i := 0
    for { } lt(i, 0x100) { } {     // while(i < 0x100)
        x := add(x, mload(i))
        i := add(i, 0x20)
    }
}

```

--------------------------------

### Solidity: Determine Winning Proposal

Source: https://docs.soliditylang.org/en/v0.8.30/solidity-by-example

Calculates and returns the index of the proposal with the highest number of votes. It iterates through all proposals to find the one with the maximum vote count.

```solidity
function winningProposal() public view
            returns (uint winningProposal_)
    {
        uint winningVoteCount = 0;
        for (uint p = 0; p < proposals.length; p++) {
            if (proposals[p].voteCount > winningVoteCount) {
                winningVoteCount = proposals[p].voteCount;
                winningProposal_ = p;
            }
        }
    }
```

--------------------------------

### Solidity Mapping Example: Balances and User Interaction

Source: https://docs.soliditylang.org/en/v0.8.30/types

Demonstrates a basic Solidity contract using a public mapping to store balances and another contract to interact with it. The `MappingExample` contract uses `mapping(address => uint) public balances` to associate addresses with unsigned integers. The `MappingUser` contract shows how to instantiate and call functions on `MappingExample`.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

contract MappingExample {
    mapping(address => uint) public balances;

    function update(uint newBalance) public {
        balances[msg.sender] = newBalance;
    }
}

contract MappingUser {
    function f() public returns (uint) {
        MappingExample m = new MappingExample();
        m.update(100);
        return m.balances(address(this));
    }
}

```

--------------------------------

### JavaScript Interaction with Solidity Coin Contract

Source: https://docs.soliditylang.org/en/v0.8.30/introduction-to-smart-contracts

Example JavaScript code using web3.js to listen for 'Sent' events from the Solidity 'Coin' contract and display transaction details. It also shows how to call the automatically generated 'balances' function.

```javascript
Coin.Sent().watch({}, '', function(error, result) {
    if (!error) {
        console.log("Coin transfer: " + result.args.amount +
            " coins were sent from " + result.args.from +
            " to " + result.args.to + ".");
        console.log("Balances now:\n" +
            "Sender: " + Coin.balances.call(result.args.from) +
            "Receiver: " + Coin.balances.call(result.args.to));
    }
})

```

--------------------------------

### Solidity preincr_u8 function example

Source: https://docs.soliditylang.org/en/v0.8.30/ir-breaking-changes

Demonstrates the behavior of the preincr_u8 function with different code generators. It shows the calculation and the unpredictability of the return value.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.1;
contract C {
    function preincr_u8(uint8 a) public pure returns (uint8) {
        return ++a + a;
    }
}
```

--------------------------------

### Solidity Short Function Declaration

Source: https://docs.soliditylang.org/en/v0.8.30/style-guide

Illustrates the permissible single-line declaration for short Solidity functions containing only a single statement. This is a stylistic choice for improving conciseness.

```solidity
function shortFunction() public { doSomething(); }
```

--------------------------------

### Example Yul Contract Object

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Illustrates a Yul object structure for a Solidity contract, including constructor code, runtime code, and embedded contract objects. It demonstrates the use of datacopy, dataoffset, and datasize for accessing data sections.

```yul
// A contract consists of a single object with sub-objects representing
// the code to be deployed or other contracts it can create.
// The single "code" node is the executable code of the object.
// Every (other) named object or data section is serialized and
// made accessible to the special built-in functions datacopy / dataoffset / datasize
// The current object, sub-objects and data items inside the current object
// are in scope.
object "Contract1" {
    // This is the constructor code of the contract.
    code {
        function allocate(size) -> ptr {
            ptr := mload(0x40)
            // Note that Solidity generated IR code reserves memory offset ``0x60`` as well, but a pure Yul object is free to use memory as it chooses.
            if iszero(ptr) { ptr := 0x60 }
            mstore(0x40, add(ptr, size))
        }

        // first create "Contract2"
        let size := datasize("Contract2")
        let offset := allocate(size)
        // This will turn into codecopy for EVM
        datacopy(offset, dataoffset("Contract2"), size)
        // constructor parameter is a single number 0x1234
        mstore(add(offset, size), 0x1234)
        pop(create(0, offset, add(size, 32)))

        // now return the runtime object (the currently
        // executing code is the constructor code)
        size := datasize("Contract1_deployed")
        offset := allocate(size)
        // This will turn into a codecopy for EVM
        datacopy(offset, dataoffset("Contract1_deployed"), size)
        return(offset, size)
    }

    data "Table2" hex"4123"

    object "Contract1_deployed" {
        code {
            function allocate(size) -> ptr {
                ptr := mload(0x40)
                // Note that Solidity generated IR code reserves memory offset ``0x60`` as well, but a pure Yul object is free to use memory as it chooses.
                if iszero(ptr) { ptr := 0x60 }
                mstore(0x40, add(ptr, size))
            }

            // runtime code

            mstore(0, "Hello, World!")
            return(0, 0x20)
        }
    }

    // Embedded object. Use case is that the outside is a factory contract,
    // and Contract2 is the code to be created by the factory
    object "Contract2" {
        code {
            // code here ...
        }

        object "Contract2_deployed" {
            code {
                // code here ...
            }
        }

        data "Table1" hex"4123"
    }
}

```

--------------------------------

### Modifier Order for Solidity Functions

Source: https://docs.soliditylang.org/en/v0.8.30/style-guide

Illustrates the recommended order for modifiers in Solidity function declarations: Visibility, Mutability, Virtual, Override, Custom modifiers.

```solidity
function balance(uint from) public view override returns (uint)  {
    return balanceOf[from];
}

function increment(uint x) public pure onlyOwner returns (uint) {
    return x + 1;
}
```

--------------------------------

### Solidity SimpleStorage Contract

Source: https://docs.soliditylang.org/en/v0.8.30/introduction-to-smart-contracts

A basic Solidity contract demonstrating state storage and retrieval. It includes functions to set and get an unsigned integer value. This contract is designed for Solidity versions between 0.4.16 and 0.9.0.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract SimpleStorage {
    uint storedData;

    function set(uint x) public {
        storedData = x;
    }

    function get() public view returns (uint) {
        return storedData;
    }
}
```

--------------------------------

### Solidity ABI JSON Representation

Source: https://docs.soliditylang.org/en/v0.8.30/abi-spec

The JSON output representing the ABI of the example Solidity contract, detailing its functions, events, and errors.

```JSON
[{
"type":"error",
"inputs": [{"name":"available","type":"uint256"},{"name":"required","type":"uint256"}],
"name":"InsufficientBalance"
}, { 
"type":"event",
"inputs": [{"name":"a","type":"uint256","indexed":true},{"name":"b","type":"bytes32","indexed":false}],
"name":"Event"
}, {
"type":"event",
"inputs": [{"name":"a","type":"uint256","indexed":true},{"name":"b","type":"bytes32","indexed":false}],
"name":"Event2"
}, {
"type":"function",
"inputs": [{"name":"a","type":"uint256"}],
"name":"foo",
"outputs": []
}]

```

--------------------------------

### Provide Solidity Source via Standard Input

Source: https://docs.soliditylang.org/en/v0.8.30/path-resolution

Redirects Solidity code to the compiler's standard input using the 'echo' command and the '-' argument. The content is placed in the virtual filesystem under the '<stdin>' source unit name.

```shell
echo 'import "./util.sol"; contract C {}' | solc -

```

--------------------------------

### Solidity Whitespace Exceptions

Source: https://docs.soliditylang.org/en/v0.8.30/style-guide

Shows exceptions to the general whitespace rules in Solidity, specifically for single-line function declarations and the omission of braces for single-statement control structures.

```solidity
function singleLine() public { spam(); }

```

```solidity
if (x < 10)
    x += 1;

```

--------------------------------

### Long Function Declarations with Modifiers in Solidity

Source: https://docs.soliditylang.org/en/v0.8.30/style-guide

Shows how to format long function declarations with multiple modifiers in Solidity, placing each modifier on a new line.

```solidity
function thisFunctionNameIsReallyLong(address x, address y, address z)
    public
    onlyOwner
    priced
    returns (address)
{
    doSomething();
}

function thisFunctionNameIsReallyLong(
    address x,
    address y,
    address z
)
    public
    onlyOwner
    priced
    returns (address)
{
    doSomething();
}
```

--------------------------------

### Solidity Function Declaration Example

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Illustrates a function declaration without an implementation body in Solidity. This syntax is used within abstract contracts to define function signatures.

```solidity
function foo(address) external returns (address);
```

--------------------------------

### Solidity Emittable Contract Example

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

A simple Solidity contract demonstrating event emission and inheritance, showing how a base contract can define a virtual function for derived contracts to override.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

contract Owned {
    address payable owner;
    constructor() { owner = payable(msg.sender); }
}

contract Emittable is Owned {
    event Emitted();

    function emitEvent() virtual public {
        if (msg.sender == owner) {
            emit Emitted();
        }
    }
}

```

--------------------------------

### Solidity Import Statements

Source: https://docs.soliditylang.org/en/v0.8.30/path-resolution

Demonstrates direct and relative import paths in Solidity. './math/math.sol' and 'contracts/tokens/token.sol' are import paths that translate to specific source unit names.

```solidity
import "./math/math.sol";
import "contracts/tokens/token.sol";


```

--------------------------------

### Solidity Contract: Full Payment Channel Implementation

Source: https://docs.soliditylang.org/en/v0.8.30/solidity-by-example

This Solidity code defines a comprehensive smart contract for a payment channel. It includes ownership management, a freeze mechanism, and core logic for claiming payments using signed messages. The contract handles nonce management to prevent replay attacks and ensures that only the owner can freeze the contract and reclaim funds.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

contract Owned {
    address payable owner;
    constructor() {
        owner = payable(msg.sender);
    }
}

contract Freezable is Owned {
    bool private _frozen = false;

    modifier notFrozen() {
        require(!_frozen, "Inactive Contract.");
        _;
    }

    function freeze() internal {
        if (msg.sender == owner)
            _frozen = true;
    }
}

contract ReceiverPays is Freezable {
    mapping(uint256 => bool) usedNonces;

    constructor() payable {}

    function claimPayment(uint256 amount, uint256 nonce, bytes memory signature)
        external
        notFrozen
    {
        require(!usedNonces[nonce]);
        usedNonces[nonce] = true;

        // this recreates the message that was signed on the client
        bytes32 message = prefixed(keccak256(abi.encodePacked(msg.sender, amount, nonce, this)));
        require(recoverSigner(message, signature) == owner);
        payable(msg.sender).transfer(amount);
    }

    /// freeze the contract and reclaim the leftover funds.
    function shutdown()
        external
        notFrozen
    {
        require(msg.sender == owner);
        freeze();
        payable(msg.sender).transfer(address(this).balance);
    }

    /// signature methods.
    function splitSignature(bytes memory sig)
        internal
        pure
        returns (uint8 v, bytes32 r, bytes32 s)
    {
        require(sig.length == 65);

        assembly {
            // first 32 bytes, after the length prefix.
            r := mload(add(sig, 32))
            // second 32 bytes.
            s := mload(add(sig, 64))
            // final byte (first byte of the next 32 bytes).
            v := byte(0, mload(add(sig, 96)))
        }

        return (v, r, s);
    }

    function recoverSigner(bytes32 message, bytes memory sig) 
        internal
        pure
        returns (address)
    {
        (uint8 v, bytes32 r, bytes32 s) = splitSignature(sig);
        return ecrecover(message, v, r, s);
    }

    /// builds a prefixed hash to mimic the behavior of eth_sign.
    function prefixed(bytes32 hash) internal pure returns (bytes32) {
        return keccak256(abi.encodePacked("\x19Ethereum Signed Message:\n32", hash));
    }
}
```

--------------------------------

### Initialize Virtual Filesystem with Standard JSON Input

Source: https://docs.soliditylang.org/en/v0.8.30/path-resolution

Provides initial Solidity source code content within a JSON structure for the compiler. The 'sources' dictionary defines the files and their content, used to populate the virtual filesystem.

```json
{
    "language": "Solidity",
    "sources": {
        "contract.sol": {
            "content": "import \"./util.sol\";\ncontract C {}"
        },
        "util.sol": {
            "content": "library Util {}"
        },
        "/usr/local/dapp-bin/token.sol": {
            "content": "contract Token {}"
        }
    },
    "settings": {"outputSelection": {"*": { "*": ["metadata", "evm.bytecode"]}}}
}

```

--------------------------------

### Solidity Function Overloading Example

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Demonstrates overloading a function 'f' within a Solidity contract 'A' with different parameter types (uint and uint, bool). This showcases how Solidity supports multiple functions with the same name.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract A {
    function f(uint value) public pure returns (uint out) {
        out = value;
    }

    function f(uint value, bool really) public pure returns (uint out) {
        if (really)
            out = value;
    }
}

```

--------------------------------

### Solidity Function Type Declaration Example

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Shows how to declare a variable whose type is a function type in Solidity. This is distinct from a function declaration without an implementation.

```solidity
function(address) external returns (address) foo;
```

--------------------------------

### EVM Opcodes from Yul Function Calls

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Explains how Yul functional expressions are translated into EVM opcodes. This example shows the sequence of opcodes generated for a memory store operation involving addition.

```Assembly
PUSH1 3 PUSH1 0x80 MLOAD ADD PUSH1 0x80 MSTORE
```

--------------------------------

### SSATransform Example in Solidity

Source: https://docs.soliditylang.org/en/v0.8.30/internals/optimizer

Demonstrates the SSATransform's effect on variable referencing in Yul code, showing how it introduces new variables. This transformation is often reversed by subsequent optimizations like CommonSubexpressionEliminator and UnusedPruner.

```solidity
let a := calldataload(0)
mstore(a, 1)
```

```solidity
let a_1 := calldataload(0)
let a := a_1
mstore(a_1, 1)
let a_2 := calldataload(0x20)
a := a_2
```

```solidity
let a := calldataload(0)
let a_1 := a
mstore(a_1, 1)
a := calldataload(0x20)
let a_2 := a
```

--------------------------------

### Sign Payment Message in JavaScript

Source: https://docs.soliditylang.org/en/v0.8.30/solidity-by-example

JavaScript functions to construct and sign messages for payment channels. It uses `web3.eth.personal.sign` for signing and `abi.soliditySHA3` for message construction. The contract address prevents replay attacks, and the amount specifies the Ether owed.

```javascript
function constructPaymentMessage(contractAddress, amount) {
    return abi.soliditySHA3(
        ["address", "uint256"],
        [contractAddress, amount]
    );
}

function signMessage(message, callback) {
    web3.eth.personal.sign(
        "0x" + message.toString("hex"),
        web3.eth.defaultAccount,
        callback
    );
}

// contractAddress is used to prevent cross-contract replay attacks.
// amount, in wei, specifies how much Ether should be sent.

function signPayment(contractAddress, amount, callback) {
    var message = constructPaymentMessage(contractAddress, amount);
    signMessage(message, callback);
}
```

--------------------------------

### Solidity Pure Function Example

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

A simple Solidity contract demonstrating a pure function that performs a calculation without reading or modifying state. It takes two unsigned integers and returns their product plus a constant.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.5.0 <0.9.0;

contract C {
    function f(uint a, uint b) public pure returns (uint) {
        return a * (b + 42);
    }
}

```

--------------------------------

### Link Libraries with solc File Input

Source: https://docs.soliditylang.org/en/v0.8.30/using-the-compiler

Shows how to provide library mappings to the solc compiler by referencing a file. Each line in the file should specify a library mapping.

```shell
solc --libraries fileName
```

--------------------------------

### Solidity Contract Inheritance with Constructor Arguments

Source: https://docs.soliditylang.org/en/v0.8.30/style-guide

Demonstrates how to declare a contract that inherits from multiple base contracts and passes arguments to their constructors. This snippet showcases a common pattern for setting up complex contract relationships in Solidity.

```solidity
pragma solidity ^0.8.0;

contract B {
    constructor(uint) {
    }
}

contract C {
    constructor(uint, uint) {
    }
}

contract D {
    constructor(uint) {
    }
}

contract A is B, C, D {
    uint x;

    constructor(uint param1, uint param2, uint param3, uint param4, uint param5)
        B(param1)
        C(param2, param3)
        D(param4) {
        x = param5;
    }
}
```

--------------------------------

### Solidity: Function Spacing within Contracts

Source: https://docs.soliditylang.org/en/v0.8.30/style-guide

Illustrates proper spacing between function declarations within a Solidity contract. A single blank line separates functions.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

abstract contract A {
    function spam() public virtual pure;
    function ham() public virtual pure;
}


contract B is A {
    function spam() public pure override {
        // ...
    }

    function ham() public pure override {
        // ...
    }
}

```

--------------------------------

### Solidity Assembly Instructions for Keccak-256

Source: https://docs.soliditylang.org/en/v0.8.30/internals/optimizer

This snippet shows a sequence of Solidity assembly instructions, including PUSH, CALLDATALOAD, DUP2, MSTORE, and KECCAK256, used to demonstrate compile-time evaluation.

```assembly
PUSH 32
PUSH 0
CALLDATALOAD
PUSH 100
DUP2
MSTORE
KECCAK256

```

--------------------------------

### Solidity: Long Function Call Formatting

Source: https://docs.soliditylang.org/en/v0.8.30/style-guide

Shows the recommended way to format long function calls in Solidity to improve readability. Each argument should be on a new line, aligned with one indent.

```Solidity
thisFunctionCallIsReallyLong(
    longArgument1,
    longArgument2,
    longArgument3
);

```

--------------------------------

### Function Specialization Example

Source: https://docs.soliditylang.org/en/v0.8.30/internals/optimizer

Illustrates function specialization, where a function is adapted to literal arguments. A function `f(a, b)` called with `f(x, 5)` is transformed into `f_1(a_1)` with `b_1` set to 5 internally, enabling further simplifications.

```solidity
function f_1(a_1) {
    let b_1 := 5
    sstore(a_1, b_1)
}
```

--------------------------------

### Solidity: Cast Vote for Proposal

Source: https://docs.soliditylang.org/en/v0.8.30/solidity-by-example

Allows a voter to cast their vote for a specific proposal. It validates the voter's eligibility and vote status, then updates the proposal's vote count.

```solidity
function vote(uint proposal) external {
        Voter storage sender = voters[msg.sender];
        require(sender.weight != 0, "Has no right to vote");
        require(!sender.voted, "Already voted.");
        sender.voted = true;
        sender.vote = proposal;

        // If `proposal` is out of the range of the array,
        // this will throw automatically and revert all
        // changes.
        proposals[proposal].voteCount += sender.weight;
    }
```

--------------------------------

### Solidity Control Structure Formatting

Source: https://docs.soliditylang.org/en/v0.8.30/style-guide

Illustrates the correct formatting for Solidity control structures (if, else, while, for) and block-level statements. Braces should open on the same line as the declaration and close on their own line, with specific spacing rules applied.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

contract Coin {
    struct Bank {
        address owner;
        uint balance;
    }
}

```

```solidity
if (...) {
    ...
}

for (...) {
    ...
}

```

```solidity
if (x < 3) {
    x += 1;
} else if (x > 7) {
    x -= 1;
} else {
    x = 5;
}


if (x < 3)
    x += 1;
else
    x -= 1;

```

--------------------------------

### Solidity: Multiply by two using verbatim

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Example demonstrating the use of `verbatim_1i_1o` in Solidity to create bytecode that multiplies an input by two, preventing the optimizer from altering the constant value.

```Solidity
let x := calldataload(0)
let double := verbatim_1i_1o(hex"600202", x)
```

--------------------------------

### Sign Payment Data with Web3.js (EIP-712 Style)

Source: https://docs.soliditylang.org/en/v0.8.30/solidity-by-example

This JavaScript function creates a signature for a payment transaction. It uses `abi.soliditySHA3` to hash the recipient's address, amount, a nonce, and the contract address, mimicking Solidity's `keccak256` with `abi.encodePacked`. The resulting hash is then signed using `web3.eth.personal.sign`.

```javascript
// recipient is the address that should be paid.
// amount, in wei, specifies how much ether should be sent.
// nonce can be any unique number to prevent replay attacks
// contractAddress is used to prevent cross-contract replay attacks
function signPayment(recipient, amount, nonce, contractAddress, callback) {
    var hash = "0x" + abi.soliditySHA3(
        ["address", "uint256", "uint256", "address"],
        [recipient, amount, nonce, contractAddress]
    ).toString("hex");

    web3.eth.personal.sign(hash, web3.eth.defaultAccount, callback);
}
```

--------------------------------

### Solidity Incorrect Contract Naming (lowercase)

Source: https://docs.soliditylang.org/en/v0.8.30/style-guide

Illustrates an incorrect naming convention where a contract and its associated filename use lowercase, which is against the recommended CapWords style in Solidity.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

// owned.sol
contract owned {
    address public owner;

    modifier onlyOwner {
        require(msg.sender == owner);
        _;
    }

    constructor() {
        owner = msg.sender;
    }

    function transferOwnership(address newOwner) public onlyOwner {
        owner = newOwner;
    }
}

```

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.7.0;


import "./owned.sol";


contract Congress is owned, tokenRecipient {
    //...
}

```

--------------------------------

### Solidity Source File Definition (URLs)

Source: https://docs.soliditylang.org/en/v0.8.30/using-the-compiler

Specifies how to provide Solidity source code using URLs. Supports multiple URLs for redundancy and an optional keccak256 hash for verification. Filesystem paths are also supported in CLI environments.

```json
{
  "keccak256": "0x123...",
  "urls": [
    "bzzr://56ab...",
    "ipfs://Qma...",
    "/tmp/path/to/file.sol"
  ]
}
```

--------------------------------

### Solidity ecrecover function example

Source: https://docs.soliditylang.org/en/v0.8.30/smtchecker

Demonstrates the use of the `ecrecover` function in Solidity. It shows how multiple calls to `ecrecover` with identical parameters are proven to return the same address, illustrating the concept of abstracting deterministic functions with uninterpreted functions.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.0;

contract Recover
{
    function f(
        bytes32 hash,
        uint8 v1, uint8 v2,
        bytes32 r1, bytes32 r2,
        bytes32 s1, bytes32 s2
    ) public pure returns (address) {
        address a1 = ecrecover(hash, v1, r1, s1);
        require(v1 == v2);
        require(r1 == r2);
        require(s1 == s2);
        address a2 = ecrecover(hash, v2, r2, s2);
        assert(a1 == a2);
        return a1;
    }
}

```

--------------------------------

### Solidity Import with Relative Path Remapping

Source: https://docs.soliditylang.org/en/v0.8.30/path-resolution

An example of a Solidity import statement that uses a relative path, which is then affected by remappings. The import './util.sol' is resolved to 'b/util.sol' due to the prior remapping configuration.

```solidity
import "./util.sol" as util; // source unit name: b/util.sol
```

--------------------------------

### Solidity Return Data (return)

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Terminates the execution of the current contract and returns data from memory. It takes a pointer to the start of the data in memory and the size of the data.

```Solidity
return(memory_pointer, data_size);
```

--------------------------------

### Solidity Import Statement with Remapping

Source: https://docs.soliditylang.org/en/v0.8.30/path-resolution

Demonstrates how to use an import statement in a Solidity file, with a remapped source unit name pointing to a different file path.

```solidity
import "/project/util.sol" as util; // source unit name: /contractsutil.sol
```

--------------------------------

### Solidity: Placing a Bid

Source: https://docs.soliditylang.org/en/v0.8.30/solidity-by-example

An internal function to place a bid in the auction. It checks if the new bid value is higher than the current highest bid. If so, it refunds the previous highest bidder and updates the highest bid and bidder.

```solidity
function placeBid(address bidder, uint value) internal
            returns (bool success)
    {
        if (value <= highestBid) {
            return false;
        }
        if (highestBidder != address(0)) {
            // Refund the previously highest bidder.
            pendingReturns[highestBidder] += highestBid;
        }
        highestBid = value;
        highestBidder = bidder;
        return true;
    }
```

--------------------------------

### Block Flattening Example

Source: https://docs.soliditylang.org/en/v0.8.30/internals/optimizer

Demonstrates how the BlockFlattener eliminates nested blocks by merging their statements into the outer block. This simplification is safe due to variable scope expansion, provided the code is disambiguated.

```solidity
{
    {
        let x := 2
        {
            let y := 3
            mstore(x, y)
        }
    }
}
```

```solidity
{
    {
        let x := 2
        let y := 3
        mstore(x, y)
    }
}
```

--------------------------------

### Solidity Implicit Type Conversion Example

Source: https://docs.soliditylang.org/en/v0.8.30/types

Demonstrates an implicit type conversion in Solidity where a uint8 variable is converted to uint16 for an addition operation. The result is then implicitly converted to uint32 for assignment.

```solidity
uint8 y;
uint16 z;
uint32 x = y + z;

```

--------------------------------

### Solidity Voting Contract Structure and Constructor

Source: https://docs.soliditylang.org/en/v0.8.30/solidity-by-example

Defines the data structures for voters and proposals, and the constructor for initializing the ballot contract. It sets the chairperson, grants them voting weight, and populates the proposals array based on provided names.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;
/// @title Voting with delegation.
contract Ballot {
    // This declares a new complex type which will
    // be used for variables later.
    // It will represent a single voter.
    struct Voter {
        uint weight; // weight is accumulated by delegation
        bool voted;  // if true, that person already voted
        address delegate; // person delegated to
        uint vote;   // index of the voted proposal
    }

    // This is a type for a single proposal.
    struct Proposal {
        bytes32 name;   // short name (up to 32 bytes)
        uint voteCount; // number of accumulated votes
    }

    address public chairperson;

    // This declares a state variable that
    // stores a `Voter` struct for each possible address.
    mapping(address => Voter) public voters;

    // A dynamically-sized array of `Proposal` structs.
    Proposal[] public proposals;

    /// Create a new ballot to choose one of `proposalNames`.
    constructor(bytes32[] memory proposalNames) {
        chairperson = msg.sender;
        voters[chairperson].weight = 1;

        // For each of the provided proposal names,
        // create a new proposal object and add it
        // to the end of the array.
        for (uint i = 0; i < proposalNames.length; i++) {
            // `Proposal({...})` creates a temporary
            // Proposal object and `proposals.push(...)`
            // appends it to the end of `proposals`.
            proposals.push(Proposal({
                name: proposalNames[i],
                voteCount: 0
            }));
        }
    }

```

--------------------------------

### Yul - Typed Literals (Illustrative Example)

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Illustrates the concept of typed literals in Yul, showing how to specify types like u32 and u256. Note that type checking for these specific types is not yet implemented.

```Yul
// This will not compile (u32 and u256 type not implemented yet)
let x := and("abc":u32, add(3:u256, 2:u256))
```

--------------------------------

### Basic Solidity Contract with Visibility

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

A foundational Solidity contract showcasing `private` and `public` state variables, and a `private` function. It illustrates how public state variables automatically get getter functions.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract C {
    function f(uint a) private pure returns (uint b) { return a + 1; }
    function setData(uint a) internal { data = a; }
    uint public data;
}
```

--------------------------------

### Solidity Aliasing Example with SMTChecker Considerations

Source: https://docs.soliditylang.org/en/v0.8.30/smtchecker

Demonstrates aliasing for reference types in Solidity and how assignments to memory or storage references affect the SMTChecker's knowledge. It highlights potential false positives due to aliasing.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.0;

contract Aliasing
{
    uint[] array1;
    uint[][] array2;
    function f(
        uint[] memory a,
        uint[] memory b,
        uint[][] memory c,
        uint[] storage d
    ) internal {
        array1[0] = 42;
        a[0] = 2;
        c[0][0] = 2;
        b[0] = 1;
        // Erasing knowledge about memory references should not
        // erase knowledge about state variables.
        assert(array1[0] == 42);
        // However, an assignment to a storage reference will erase
        // storage knowledge accordingly.
        d[0] = 2;
        // Fails as false positive because of the assignment above.
        assert(array1[0] == 42);
        // Fails because `a == b` is possible.
        assert(a[0] == 2);
        // Fails because `c[i] == b` is possible.
        assert(c[0][0] == 2);
        assert(d[0] == 2);
        assert(b[0] == 1);
    }
    function g(
        uint[] memory a,
        uint[] memory b,
        uint[][] memory c,
        uint x
    ) public {
        f(a, b, c, array2[x]);
    }
}

```

--------------------------------

### Compiler Settings - General

Source: https://docs.soliditylang.org/en/v0.8.30/using-the-compiler

Configures general compiler settings, including the stage at which compilation should stop and a list of remappings for import paths.

```json
{
  "stopAfter": "parsing",
  "remappings": [ ":g=/dir" ]
}
```

--------------------------------

### Solidity: Auction Ending and Bid Transfer

Source: https://docs.soliditylang.org/en/v0.8.30/solidity-by-example

Allows the auction to be ended after a specific reveal period. It emits an 'AuctionEnded' event and transfers the highest bid amount to the designated beneficiary.

```solidity
function auctionEnd()
        external
        onlyAfter(revealEnd) 
    {
        if (ended) revert AuctionEndAlreadyCalled();
        emit AuctionEnded(highestBidder, highestBid);
        ended = true;
        beneficiary.transfer(highestBid);
    }
```

--------------------------------

### Solidity abi.encodePacked() Padding Example

Source: https://docs.soliditylang.org/en/v0.8.30/abi-spec

Illustrates how explicit type conversions can be used for padding in Solidity's packed encoding. This is useful when padding is required for specific types.

```Solidity
abi.encodePacked(uint16(0x12)) == hex"0012"
```

--------------------------------

### Specify Source URLs with Standard JSON Input

Source: https://docs.soliditylang.org/en/v0.8.30/path-resolution

Uses Standard JSON to define source files via URLs, allowing the compiler to fetch content through an import callback. The 'sources' dictionary keys serve as source unit names.

```json
{
    "language": "Solidity",
    "sources": {
        "/usr/local/dapp-bin/token.sol": {
            "urls": [
                "/projects/mytoken.sol",
                "https://example.com/projects/mytoken.sol"
            ]
        }
    },
    "settings": {"outputSelection": {"*": { "*": ["metadata", "evm.bytecode"]}}}
}

```

--------------------------------

### Solidity: Delegate Voting Logic

Source: https://docs.soliditylang.org/en/v0.8.30/solidity-by-example

Handles the logic for delegates voting, including adding to their weight if they haven't voted yet. It ensures that only eligible voters can cast their votes and prevents double voting.

```solidity
function delegate(uint voter) {
        // ... existing code ...
        if (delegate_.weight != 0) {
            // If the delegate did not vote yet,
            // add to her weight.
            delegate_.weight += sender.weight;
        }
    }
```

--------------------------------

### Solidity Address Conversion Example

Source: https://docs.soliditylang.org/en/v0.8.30/080-breaking-changes

Demonstrates explicit conversion of a contract address to a payable address type in Solidity. This is useful when the contract might not inherently support Ether reception.

```Solidity
payable(address(c))
```

--------------------------------

### Solidity: Bid Withdrawal Logic

Source: https://docs.soliditylang.org/en/v0.8.30/solidity-by-example

Handles the withdrawal of bids that were overbid. It checks for pending returns for the sender, resets the pending return amount to zero to prevent re-entrancy issues, and then transfers the owed amount.

```solidity
function withdraw() external {
        uint amount = pendingReturns[msg.sender];
        if (amount > 0) {
            // It is important to set this to zero because the recipient
            // can call this function again as part of the receiving call
            // before `transfer` returns (see the remark above about
            // conditions -> effects -> interaction).
            pendingReturns[msg.sender] = 0;

            payable(msg.sender).transfer(amount);
        }
    }
```

--------------------------------

### Solidity Integer Division Rounding

Source: https://docs.soliditylang.org/en/v0.8.30/types

Explains that integer division in Solidity always results in an integer, rounding towards zero. Provides an example of negative number division.

```solidity
int256(-5) / int256(2) == int256(-2);
```

--------------------------------

### Solidity Overload Resolution Argument Matching Example

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Shows how Solidity resolves overloaded functions based on argument matching. It highlights that if an argument can be implicitly converted to multiple parameter types, it leads to a type error, but if only one match exists, it resolves correctly.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract A {
    function f(uint8 val) public pure returns (uint8 out) {
        out = val;
    }

    function f(uint256 val) public pure returns (uint256 out) {
        out = val;
    }
}

```

--------------------------------

### Solidity Function Ordering by Visibility

Source: https://docs.soliditylang.org/en/v0.8.30/style-guide

Demonstrates the recommended order for functions within a Solidity contract. Functions should be grouped by visibility (constructor, receive, fallback, external, public, internal, private) and sorted, with view and pure functions placed last within their visibility groups.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;
contract A {
    constructor() {
        // ...
    }

    receive() external payable {
        // ...
    }

    fallback() external {
        // ...
    }

    // External functions
    // ...

    // External functions that are view
    // ...

    // External functions that are pure
    // ...

    // Public functions
    // ...

    // Internal functions
    // ...

    // Private functions
    // ...
}

```

--------------------------------

### Solidity Array Memory Layout Example

Source: https://docs.soliditylang.org/en/v0.8.30/internals/layout_in_memory

Demonstrates the difference in memory allocation for a Solidity array. A uint8[4] array occupies 128 bytes in memory, unlike its storage representation.

```solidity
uint8[4] a;

```

--------------------------------

### Solidity Contract Storage Layout Example

Source: https://docs.soliditylang.org/en/v0.8.30/internals/layout_in_storage

Demonstrates the storage layout of a Solidity contract with inheritance and a custom layout. It shows how state variables are packed into storage slots, considering their types, size, and placement rules for structs and arrays.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.29;

struct S {
    int32 x;
    bool y;
}

contract A {
    uint a;
    uint128 transient b;
    uint constant c = 10;
    uint immutable d = 12;
}

contract B {
    uint8[] e;
    mapping(uint => S) f;
    uint16 g;
    uint16 h;
    bytes16 transient i;
    S s;
    int8 k;
}

contract C is A, B layout at 42 {
    bytes21 l;
    uint8[10] m;
    bytes5[8] n;
    bytes5 o;
}

```

--------------------------------

### Solidity Enum Usage Example

Source: https://docs.soliditylang.org/en/v0.8.30/types

Illustrates the definition and usage of an enum type in Solidity. It includes setting enum values, returning them, and accessing the minimum and maximum values of an enum. Enums are value types and can be converted to and from integers.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.8;

contract test {
    enum ActionChoices { GoLeft, GoRight, GoStraight, SitStill }
    ActionChoices choice;
    ActionChoices constant defaultChoice = ActionChoices.GoStraight;

    function setGoStraight() public {
        choice = ActionChoices.GoStraight;
    }

    // Since enum types are not part of the ABI, the signature of "getChoice"
    // will automatically be changed to "getChoice() returns (uint8)"
    // for all matters external to Solidity.
    function getChoice() public view returns (ActionChoices) {
        return choice;
    }

    function getDefaultChoice() public pure returns (uint) {
        return uint(defaultChoice);
    }

    function getLargestValue() public pure returns (ActionChoices) {
        return type(ActionChoices).max;
    }

    function getSmallestValue() public pure returns (ActionChoices) {
        return type(ActionChoices).min;
    }
}
```

--------------------------------

### Solidity Custom Storage Layout

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Demonstrates how to define an arbitrary storage location for a contract's state variables using the 'layout at' specifier. This shifts the starting slot for all state variables, including inherited ones, from the default zero.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.29;

contract C layout at 0xAAAA + 0x11 {
    uint[3] x; // Occupies slots 0xAABB..0xAABD
}

```

--------------------------------

### Solidity Storage Layout - Type Information Example

Source: https://docs.soliditylang.org/en/v0.8.30/internals/layout_in_storage

Illustrates the format of an entry in the 'types' object of the JSON output. This section provides detailed information about the data types used in the contract, including encoding method, canonical label, and size in bytes.

```json
{
    "encoding": "inplace",
    "label": "uint256",
    "numberOfBytes": "32"
}
```

--------------------------------

### Solidity: Override Function Mutability and Visibility

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Demonstrates overriding a virtual function to change its visibility from external to public and mutability from view to pure. This is a fundamental example of function overriding in Solidity.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

contract Base
{
    function foo() virtual external view {}
}

contract Middle is Base {}

contract Inherited is Middle
{
    function foo() override public pure {}
}

```

--------------------------------

### Solidity Revert with Data (revert)

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Terminates the execution, reverts any state changes made during the current transaction, and returns data from memory. It takes a pointer to the start of the data and the size of the data.

```Solidity
revert(memory_pointer, data_size);
// Example usage:
// require(condition, "Error message"); // This compiles to revert
```

--------------------------------

### AFL Fuzzer Error: Binary Not Instrumented

Source: https://docs.soliditylang.org/en/v0.8.30/contributing

An example error message from afl-fuzz indicating that the target binary is not instrumented, which is required for effective fuzzing. It suggests checking README for instrumentation tips or using QEMU mode.

```text
afl-fuzz 2.52b by <lcamtuf@google.com>
... (truncated messages)
[*] Validating target binary...

[-] Looks like the target binary is not instrumented! The fuzzer depends on
    compile-time instrumentation to isolate interesting test cases while
    mutating the input data. For more information, and for tips on how to
    instrument binaries, please see /usr/share/doc/afl-doc/docs/README.

    When source code is not available, you may be able to leverage QEMU
    mode support. Consult the README for tips on how to enable this.
    (It is also possible to use afl-fuzz as a traditional, "dumb" fuzzer.
    For that, you can use the -n option - but expect much worse results.)

[-] PROGRAM ABORT : No instrumentation detected
         Location : check_binary(), afl-fuzz.c:6920
```

--------------------------------

### Solidity: Multiply Modulo

Source: https://docs.soliditylang.org/en/v0.8.30/units-and-global-variables

Computes (x * y) % k with arbitrary precision multiplication that does not wrap around at 2**256. Asserts k != 0 starting from version 0.5.0.

```Solidity
mulmod(uint x, uint y, uint k) returns (uint)
```

--------------------------------

### Solidity Proxy Contract Example

Source: https://docs.soliditylang.org/en/v0.8.30/security-considerations

Demonstrates a Solidity contract acting as a proxy, forwarding calls to another address with specified payload. It includes a function to call external contracts and a separate contract for the actual proxy functionality.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.0;
contract ProxyWithMoreFunctionality {
    PermissionlessProxy proxy;

    function callOther(address addr, bytes memory payload) public
            returns (bool, bytes memory) {
        return proxy.callOther(addr, payload);
    }
    // Other functions and other functionality
}

// This is the full contract, it has no other functionality and
// requires no privileges to work.
contract PermissionlessProxy {
    function callOther(address addr, bytes memory payload) public
            returns (bool, bytes memory) {
        return addr.call(payload);
    }
}

```

--------------------------------

### Solidity Custom Error Example

Source: https://docs.soliditylang.org/en/v0.8.30/abi-spec

Demonstrates defining and reverting a custom error 'InsufficientBalance' with specific arguments in a Solidity contract. The revert data includes the error selector and encoded arguments.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.4;

contract TestToken {
    error InsufficientBalance(uint256 available, uint256 required);
    function transfer(address /*to*/, uint amount) public pure {
        revert InsufficientBalance(0, amount);
    }
}

```

--------------------------------

### Solidity: Recovering the Signer Address

Source: https://docs.soliditylang.org/en/v0.8.30/solidity-by-example

This function recovers the Ethereum address of the signer from a message hash and its corresponding ECDSA signature. It utilizes the `splitSignature` function to parse the signature and then employs the built-in `ecrecover` precompile.

```Solidity
function recoverSigner(bytes32 message, bytes memory sig) 
    internal
    pure
    returns (address)
{
    (uint8 v, bytes32 r, bytes32 s) = splitSignature(sig);
    return ecrecover(message, v, r, s);
}
```

--------------------------------

### Solidity: costs Modifier with Arguments Example

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Illustrates a 'costs' modifier that accepts an argument ('price'). It checks if the Ether sent ('msg.value') is sufficient to cover the specified price before executing the function body.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.1 <0.9.0;

contract priced {
    // Modifiers can receive arguments:
    modifier costs(uint price) {
        if (msg.value >= price) {
            _;
        }
    }
}

contract Register is priced {
    mapping(address => bool) registeredAddresses;
    uint price;

    constructor(uint initialPrice) { price = initialPrice; }

    // It is important to also provide the
    // `payable` keyword here, otherwise the function will
    // automatically reject all Ether sent to it.
    function register() public payable costs(price) {
        registeredAddresses[msg.sender] = true;
    }
}
```

--------------------------------

### Solidity Inheritance with Super for Correct Event Chaining

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

This Solidity example demonstrates the correct way to handle event emission across multiple inheritance levels using the `super` keyword. By using `super.emitEvent()`, the contract ensures that functions in all parent contracts are called in the correct order, preventing skipped logic.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

contract Owned {
    address payable owner;
    constructor() { owner = payable(msg.sender); }
}

contract Emittable is Owned {
    event Emitted();

    function emitEvent() virtual public {
        if (msg.sender == owner) {
            emit Emitted();
        }
    }
}

contract Base1 is Emittable {
    event Base1Emitted();
    function emitEvent() public virtual override {
        /* Here, we emit an event to simulate some Base1 logic */
        emit Base1Emitted();
        super.emitEvent();
    }
}


contract Base2 is Emittable {
    event Base2Emitted();
    function emitEvent() public virtual override {
        /* Here, we emit an event to simulate some Base2 logic */
        emit Base2Emitted();
        super.emitEvent();
    }
}

contract Final is Base1, Base2 {
    event FinalEmitted();
    function emitEvent() public override(Base1, Base2) {
        /* Here, we emit an event to simulate some Final logic */
        emit FinalEmitted();
        super.emitEvent();
    }
}
```

--------------------------------

### Solidity: Add Modulo

Source: https://docs.soliditylang.org/en/v0.8.30/units-and-global-variables

Computes (x + y) % k with arbitrary precision addition that does not wrap around at 2**256. Asserts k != 0 starting from version 0.5.0.

```Solidity
addmod(uint x, uint y, uint k) returns (uint)
```

--------------------------------

### Solidity Overflow Check Example

Source: https://docs.soliditylang.org/en/v0.8.30/smtchecker

Demonstrates an overflow check in Solidity. The SMTChecker requires specific command-line or JSON options to detect underflow and overflow for versions >=0.8.7. This contract shows a basic addition that can lead to overflow.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.0;

contract Overflow {
    uint immutable x;
    uint immutable y;

    function add(uint x_, uint y_) internal pure returns (uint) {
        return x_ + y_;
    }

    constructor(uint x_, uint y_) {
        (x, y) = (x_, y_);
    }

    function stateAdd() public view returns (uint) {
        return add(x, y);
    }
}

```

--------------------------------

### Yul Power Function Implementation

Source: https://docs.soliditylang.org/en/v0.8.30/yul

An example of a Yul function that calculates the power of a number using a square-and-multiply algorithm. It handles base cases for exponent 0 and 1, and recursively computes the result for other exponents.

```Yul
{
    function power(base, exponent) -> result {
        switch exponent
        case 0 { result := 1 }
        case 1 { result := base }
        default {
            result := power(mul(base, base), div(exponent, 2))
            switch mod(exponent, 2)
                case 1 { result := mul(base, result) }
        }
    }
}

```

--------------------------------

### Solidity Constructor Execution Order in Inheritance

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Illustrates how constructors in Solidity are executed based on the linearized order of base contracts, not the order in which arguments are provided. This example showcases different inheritance hierarchies and their resulting constructor execution sequences.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

contract Base1 {
    constructor() {
        // Constructor logic for Base1
    }
}

contract Base2 {
    constructor() {
        // Constructor logic for Base2
    }
}

// Constructors are executed in the following order:
//  1 - Base1
//  2 - Base2
//  3 - Derived1
contract Derived1 is Base1, Base2 {
    constructor() Base1() Base2() {
        // Derived1 constructor logic
    }
}

// Constructors are executed in the following order:
//  1 - Base2
//  2 - Base1
//  3 - Derived2
contract Derived2 is Base2, Base1 {
    constructor() Base2() Base1() {
        // Derived2 constructor logic
    }
}

// Constructors are still executed in the following order:
//  1 - Base2
//  2 - Base1
//  3 - Derived3
contract Derived3 is Base2, Base1 {
    constructor() Base1() Base2() {
        // Derived3 constructor logic
    }
}
```

--------------------------------

### Solidity Yul: Declare, Use, and Store Variables

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Demonstrates declaring variables with 'let', loading data from calldata, performing arithmetic operations, loading from storage, updating variables, and storing results back into storage in Yul.

```Solidity Yul
{
    let zero := 0
    let v := calldataload(zero)
    {
        let y := add(sload(v), 1)
        v := y
    } // y is "deallocated" here
    sstore(v, zero)
} // v and zero are "deallocated" here

```

--------------------------------

### Solidity Type Conversion Example

Source: https://docs.soliditylang.org/en/v0.8.30/types

Demonstrates how number literal expressions are converted to non-literal types and the potential type compatibility issues in Solidity. The expression `2.5 + a + 0.5` requires a common type, which is not available for `2.5` and `uint128`.

```solidity
uint128 a = 1;
uint128 b = 2.5 + a + 0.5;

```

--------------------------------

### Solidity Contract Example for Storage Layout

Source: https://docs.soliditylang.org/en/v0.8.30/internals/layout_in_storage

A sample Solidity contract demonstrating various data types, including value types, reference types, packed-encoded types, and nested types. This contract is used to illustrate the JSON storage layout output.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.28;
contract A {
    struct S {
        uint128 a;
        uint128 b;
        uint[2] staticArray;
        uint[] dynArray;
    }

    uint x;
    uint transient y;
    uint w;
    uint transient z;

    S s;
    address addr;
    address transient taddr;
    mapping(uint => mapping(address => bool)) map;
    uint[] array;
    string s1;
    bytes b1;
}
```

--------------------------------

### Solidity Safe Remote Purchase Contract

Source: https://docs.soliditylang.org/en/v0.8.30/solidity-by-example

This Solidity contract implements a remote purchase mechanism. It requires both the buyer and seller to deposit funds as escrow. The contract manages the transaction lifecycle through different states and uses modifiers to enforce access control and state conditions. It handles fund transfers upon confirmation of item receipt and provides functionality for aborting the purchase.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.4;
contract Purchase {
    uint public value;
    address payable public seller;
    address payable public buyer;

    enum State { Created, Locked, Release, Inactive }
    // The state variable has a default value of the first member, `State.created`
    State public state;

    modifier condition(bool condition_) {
        require(condition_);
        _;
    }

    /// Only the buyer can call this function.
    error OnlyBuyer();
    /// Only the seller can call this function.
    error OnlySeller();
    /// The function cannot be called at the current state.
    error InvalidState();
    /// The provided value has to be even.
    error ValueNotEven();

    modifier onlyBuyer() {
        if (msg.sender != buyer)
            revert OnlyBuyer();
        _;
    }

    modifier onlySeller() {
        if (msg.sender != seller)
            revert OnlySeller();
        _;
    }

    modifier inState(State state_) {
        if (state != state_)
            revert InvalidState();
        _;
    }

    event Aborted();
    event PurchaseConfirmed();
    event ItemReceived();
    event SellerRefunded();

    // Ensure that `msg.value` is an even number.
    // Division will truncate if it is an odd number.
    // Check via multiplication that it wasn't an odd number.
    constructor() payable {
        seller = payable(msg.sender);
        value = msg.value / 2;
        if ((2 * value) != msg.value)
            revert ValueNotEven();
    }

    /// Abort the purchase and reclaim the ether.
    /// Can only be called by the seller before
    /// the contract is locked.
    function abort(
    ) 
        external
        onlySeller
        inState(State.Created)
    {
        emit Aborted();
        state = State.Inactive;
        // We use transfer here directly. It is
        // reentrancy-safe, because it is the
        // last call in this function and we
        // already changed the state.
        seller.transfer(address(this).balance);
    }

    /// Confirm the purchase as buyer.
    /// Transaction has to include `2 * value` ether.
    /// The ether will be locked until confirmReceived
    /// is called.
    function confirmPurchase(
    ) 
        external
        inState(State.Created)
        condition(msg.value == (2 * value))
        payable
    {
        emit PurchaseConfirmed();
        buyer = payable(msg.sender);
        state = State.Locked;
    }

    /// Confirm that you (the buyer) received the item.
    /// This will release the locked ether.
    function confirmReceived(
    ) 
        external
        onlyBuyer
        inState(State.Locked)
    {
        emit ItemReceived();
        // It is important to change the state first because
        // otherwise, the contracts called using `send` below
        // can call in again here.
        state = State.Release;

        buyer.transfer(value);
    }

    /// This function refunds the seller, i.e.
    /// pays back the locked funds of the seller.
    function refundSeller(
    ) 
        external
        onlySeller
        inState(State.Release)
    {
        emit SellerRefunded();
        // It is important to change the state first because
        // otherwise, the contracts called using `send` below
        // can call in again here.
        state = State.Inactive;

        seller.transfer(3 * value);
    }
}

```

--------------------------------

### Solidity: Splitting ECDSA Signature Parameters

Source: https://docs.soliditylang.org/en/v0.8.30/solidity-by-example

This function demonstrates how to split an ECDSA signature (concatenated r, s, and v) into its individual components using inline assembly. It ensures the signature is 65 bytes long and extracts r, s, and v values.

```Solidity
function splitSignature(bytes memory sig)
    internal
    pure
    returns (uint8 v, bytes32 r, bytes32 s)
{
    require(sig.length == 65);

    assembly {
        // first 32 bytes, after the length prefix.
        r := mload(add(sig, 32))
        // second 32 bytes.
        s := mload(add(sig, 64))
        // final byte (first byte of the next 32 bytes).
        v := byte(0, mload(add(sig, 96)))
    }

    return (v, r, s);
}
```

--------------------------------

### Solidity Function Signature Example

Source: https://docs.soliditylang.org/en/v0.8.30/abi-spec

Defines the canonical expression of a function's basic prototype used for generating the function selector. It includes the function name and a comma-separated list of parameter types without spaces.

```solidity
function transfer(address to, uint256 amount) public pure returns (bool success)
```

--------------------------------

### Solidity Contract Analysis Example (Solidity)

Source: https://docs.soliditylang.org/en/v0.8.30/smtchecker

Demonstrates contract analysis with SMTChecker, highlighting assertions that should hold but may fail due to limitations in analyzing external calls and state variable changes across transactions. It includes contracts A and B with constructor and function definitions.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.0;

contract A {
    uint public x;
    address immutable public owner;
    constructor() {
        owner = msg.sender;
    }
    function setX(uint _x) public {
        require(msg.sender == owner);
        x = _x;
    }
}

contract B {
    A a;
    constructor() {
        a = new A();
        assert(a.x() == 0); // (1) should hold
    }
    function g() public view {
        assert(a.owner() == address(this)); // (2) should hold
        assert(a.x() == 0); // (3) should hold, but fails due to a false positive
    }
}

```

--------------------------------

### Remapping excluding base path addition

Source: https://docs.soliditylang.org/en/v0.8.30/path-resolution

Illustrates a scenario where a remapping is used in conjunction with the `--base-path` compiler option. This example shows that the remapping `/project/=/contracts/` does not prevent the `--base-path /project` from adding '/project/' internally, leading to 'contract.sol' as the source unit name.

```bash
solc /project/=/contracts/ /project/contract.sol --base-path /project # source unit name: contract.sol
```

--------------------------------

### Reading Storage and Transient Storage in Solidity Assembly

Source: https://docs.soliditylang.org/en/v0.8.30/assembly

Shows how to read from storage slots using `.slot` and perform arithmetic operations within inline assembly. This example uses transient storage `a` and state variable `b`. Requires Solidity 0.8.28 or higher.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.28 <0.9.0;

// This will report a warning
contract C {
    bool transient a;
    uint b;
    function f(uint x) public returns (uint r) {
        assembly {
            // We ignore the storage slot offset, we know it is zero
            // in this special case.
            r := mul(x, sload(b.slot))
            tstore(a.slot, true)
        }
    }
}
```

--------------------------------

### Link Libraries with solc Command-Line

Source: https://docs.soliditylang.org/en/v0.8.30/using-the-compiler

Demonstrates how to specify library addresses directly on the solc command line for linking. Libraries can be separated by spaces or commas, and the separator between the library name and its address can be ':' or '=' (with '=' being the preferred and newer method).

```shell
solc --libraries "file.sol:Math=0x1234567890123456789012345678901234567890 file.sol:Heap=0xabCD567890123456789012345678901234567890"
```

```shell
solc --libraries "file.sol:Math:0x1234567890123456789012345678901234567890 file.sol:Heap:0xabCD567890123456789012345678901234567890"
```

--------------------------------

### Remapping with relative path prefix

Source: https://docs.soliditylang.org/en/v0.8.30/path-resolution

Demonstrates remapping that involves relative path prefixes. The remapping `./=a/` and `/project/=b/` modifies how relative paths are resolved, changing the source unit name for an import like './util.sol'.

```bash
solc ./=a/ /project/=b/ /project/contract.sol # source unit name: /project/contract.sol
```

--------------------------------

### Memory-Unsafe Assembly: returndatacopy (Solidity)

Source: https://docs.soliditylang.org/en/v0.8.30/assembly

An example of an inline assembly block in Solidity that is not memory-safe. It uses `returndatacopy` with a size that might exceed the 64-byte scratch space, potentially leading to undefined behavior.

```solidity
assembly {
  returndatacopy(0, 0, returndatasize())
  revert(0, returndatasize())
}
```

--------------------------------

### Solidity Checked vs. Unchecked Arithmetic

Source: https://docs.soliditylang.org/en/v0.8.30/types

Demonstrates how Solidity handles arithmetic operations, with default checked behavior for overflow/underflow and the option to use `unchecked` blocks for wrapping arithmetic. Includes examples of integer negation and potential issues with `type(int).min`.

```solidity
int x = type(int).min;
// In checked mode, -x will cause a failing assertion.
// In unchecked mode, unchecked { assert(-x == x); } holds.
```

--------------------------------

### Solidity: Explicit conversion to non-payable address

Source: https://docs.soliditylang.org/en/v0.8.30/080-breaking-changes

Explicit conversions into the `address` type now always return a non-payable `address`. To get a payable address, use `payable(address(variable))`.

```Solidity
address(u)
```

```Solidity
address(b)
```

```Solidity
payable(address(u))
```

```Solidity
payable(address(b))
```

--------------------------------

### Run Soltest on Windows (Command Prompt)

Source: https://docs.soliditylang.org/en/v0.8.30/contributing

Command to run the Soltest executable on Windows using the native Command Prompt, with SMT tests disabled.

```shell
.\build\test\Release\soltest.exe -- --no-smt
```

--------------------------------

### Solidity Nested Mapping for ERC20 Allowances

Source: https://docs.soliditylang.org/en/v0.8.30/types

Provides an example of nested mapping usage in Solidity, specifically for implementing the `_allowances` mechanism in an ERC20 token contract. It shows how to record and manage approvals for token transfers between different addresses.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.22 <0.9.0;

contract MappingExample {

    mapping(address => uint256) private _balances;
    mapping(address => mapping(address => uint256)) private _allowances;

    event Transfer(address indexed from, address indexed to, uint256 value);
    event Approval(address indexed owner, address indexed spender, uint256 value);

    function allowance(address owner, address spender) public view returns (uint256) {
        return _allowances[owner][spender];
    }

    function transferFrom(address sender, address recipient, uint256 amount) public returns (bool) {
        require(_allowances[sender][msg.sender] >= amount, "ERC20: Allowance not high enough.");
        _allowances[sender][msg.sender] -= amount;
        _transfer(sender, recipient, amount);
        return true;
    }

    function approve(address spender, uint256 amount) public returns (bool) {
        require(spender != address(0), "ERC20: approve to the zero address");

        _allowances[msg.sender][spender] = amount;
        emit Approval(msg.sender, spender, amount);
        return true;
    }

    function _transfer(address sender, address recipient, uint256 amount) internal {
        require(sender != address(0), "ERC20: transfer from the zero address");
        require(recipient != address(0), "ERC20: transfer to the zero address");
        require(_balances[sender] >= amount, "ERC20: Not enough funds.");

```

--------------------------------

### Solidity: View Function Example

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Shows a 'view' function in Solidity that promises not to modify the contract's state. This function performs a calculation involving input parameters and the block timestamp, returning a single unsigned integer.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.5.0 <0.9.0;

contract C {
    function f(uint a, uint b) public view returns (uint) {
        return a * (b + 42) + block.timestamp;
    }
}

```

--------------------------------

### Unchecked Loop Increment - Ineligible Type Conversion

Source: https://docs.soliditylang.org/en/v0.8.30/internals/optimizer

Example demonstrating why a loop is ineligible for unchecked increment due to type conversion. Here, `uint8` is widened to `uint16` before comparison, potentially altering loop behavior.

```Solidity
for (uint8 i = 0; i < uint16(1000); i++) {
    // ...
}
```

--------------------------------

### Solidity Simple Open Auction Contract

Source: https://docs.soliditylang.org/en/v0.8.30/solidity-by-example

This is the main Solidity smart contract for a simple open auction. It defines auction parameters like beneficiary and end time, tracks the highest bid and bidder, and includes events for bid increases and auction end. It also defines custom errors for various failure conditions. The contract prevents self-activation and requires manual calls to finalize.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.4;
contract SimpleAuction {
    // Parameters of the auction.
    address payable public beneficiary;
    uint public auctionEndTime;

    // Current state of the auction.
    address public highestBidder;
    uint public highestBid;

    // Allowed withdrawals of previous bids
    mapping(address => uint) pendingReturns;

    // Set to true at the end, disallows any change.
    bool ended;

    // Events that will be emitted on changes.
    event HighestBidIncreased(address bidder, uint amount);
    event AuctionEnded(address winner, uint amount);

    // Errors that describe failures.
    error AuctionAlreadyEnded();
    error BidNotHighEnough(uint highestBid);
    error AuctionNotYetEnded();
    error AuctionEndAlreadyCalled();

    /// Create a simple auction with `biddingTime` seconds bidding time on behalf of the beneficiary address `beneficiaryAddress`.
    constructor(
        uint biddingTime,
        address payable beneficiaryAddress
    ) {
        beneficiary = beneficiaryAddress;
        auctionEndTime = block.timestamp + biddingTime;
    }

    /// Bid on the auction with the value sent together with this transaction. The value will only be refunded if the auction is not won.
    function bid() external payable {
        if (block.timestamp > auctionEndTime)
            revert AuctionAlreadyEnded();

        if (msg.value <= highestBid)
            revert BidNotHighEnough(highestBid);

        if (highestBid != 0) {
            pendingReturns[highestBidder] += highestBid;
        }
        highestBidder = msg.sender;
        highestBid = msg.value;
        emit HighestBidIncreased(msg.sender, msg.value);
    }

    /// Withdraw a bid that was overbid.
    function withdraw() external returns (bool) {
        uint amount = pendingReturns[msg.sender];
        if (amount > 0) {
            pendingReturns[msg.sender] = 0;
            if (!payable(msg.sender).send(amount)) {
                pendingReturns[msg.sender] = amount;
                return false;
            }
        }
        return true;
    }

    /// End the auction and send the highest bid to the beneficiary.
    function auctionEnd() external {
        // It is a good guideline to structure functions that interact with other contracts (i.e. they call functions or send Ether) into three phases:
        // 1. checking conditions
        // 2. performing actions (potentially changing conditions)
        // 3. interacting with other contracts
        // If these phases are mixed up, the other contract could call back into the current contract and modify the state or cause
    }
}
```

--------------------------------

### Solidity Contract Element Ordering - Correct Usage

Source: https://docs.soliditylang.org/en/v0.8.30/style-guide

Shows the recommended order for elements within a Solidity contract, including pragma, imports, events, errors, interfaces, libraries, and contracts. It also details the internal order for contract elements: type declarations, state variables, events, errors, modifiers, and functions.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.4 <0.9.0;

abstract contract Math {
    error DivideByZero();
    function divide(int256 numerator, int256 denominator) public virtual returns (uint256);
}
```

--------------------------------

### Solidity Compiler Allowed Paths

Source: https://docs.soliditylang.org/en/v0.8.30/using-the-compiler

Demonstrates how to specify allowed directories for the Solidity compiler to access for resolving imports. The `--allow-paths` switch enables access to specific directories and their subdirectories, enhancing security and flexibility.

```bash
solc --allow-paths /sample/path,/another/sample/path sourceFile.sol
```

--------------------------------

### Solidity Internal Function Call Example

Source: https://docs.soliditylang.org/en/v0.8.30/control-structures

Demonstrates an internal function call within a Solidity contract. It shows recursive calling and the use of SPDX license identifier and pragma. Note the warning generated by the recursive structure.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.22 <0.9.0;

// This will report a warning
contract C {
    function g(uint a) public pure returns (uint ret) { return a + f(); }
    function f() internal pure returns (uint ret) { return g(7) + f(); }
}

```

--------------------------------

### Solidity: TokenCreator Contract Example

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

A Solidity contract named `TokenCreator` that demonstrates how to create new `OwnedToken` contracts. It includes a `createToken` function to deploy new tokens and a `changeName` function to modify the name of an existing token. It also features a `isTokenTransferOK` function for conditional logic.

```solidity
contract TokenCreator {
    function createToken(bytes32 name)
        public
        returns (OwnedToken tokenAddress)
    {
        // Create a new `Token` contract and return its address.
        // From the JavaScript side, the return type
        // of this function is `address`, as this is
        // the closest type available in the ABI.
        return new OwnedToken(name);
    }

    function changeName(OwnedToken tokenAddress, bytes32 name) public {
        // Again, the external type of `tokenAddress` is
        // simply `address`.
        tokenAddress.changeName(name);
    }

    // Perform checks to determine if transferring a token to the
    // `OwnedToken` contract should proceed
    function isTokenTransferOK(address currentOwner, address newOwner)
        public
        pure
        returns (bool ok)
    {
        // Check an arbitrary condition to see if transfer should proceed
        return keccak256(abi.encodePacked(currentOwner, newOwner))[0] == 0x7f;
    }
}

```

--------------------------------

### Solidity: Grant Voting Rights Function

Source: https://docs.soliditylang.org/en/v0.8.30/solidity-by-example

Allows the contract chairperson to grant voting rights to a specific address. It includes checks to ensure only the chairperson can call this function, and that the target address has not already voted and has no prior voting weight.

```solidity
// Give `voter` the right to vote on this ballot.
// May only be called by `chairperson`.
function giveRightToVote(address voter) external {
    // If the first argument of `require` evaluates
    // to `false`, execution terminates and all
    // changes to the state and to Ether balances
    // are reverted.
    // This used to consume all gas in old EVM versions, but
    // not anymore.
    // It is often a good idea to use `require` to check if
    // functions are called correctly.
    // As a second argument, you can also provide an
    // explanation about what went wrong.
    require(
        msg.sender == chairperson,
        "Only chairperson can give right to vote."
    );
    require(
        !voters[voter].voted,
        "The voter already voted."
    );
    require(voters[voter].weight == 0);
    voters[voter].weight = 1;
}

```

--------------------------------

### Solidity Yul: Conditional Execution with 'if'

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Demonstrates the use of the 'if' statement in Yul to conditionally execute code. This example checks the calldata size and reverts if it's less than 4 bytes. The curly braces for the body are mandatory.

```Solidity Yul
if lt(calldatasize(), 4) { revert(0, 0) }

```

--------------------------------

### Example of an Older Solidity Contract (Pre-0.5.0)

Source: https://docs.soliditylang.org/en/v0.8.30/050-breaking-changes

This is a sample Solidity contract written for a version prior to 0.5.0. It includes functions with `constant` specifiers, which require special handling (using `view` with caution) when defining interfaces for interoperability with newer Solidity versions.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.4.25;
// This will report a warning until version 0.4.25 of the compiler
// This will not compile after 0.5.0
contract OldContract {
    function someOldFunction(uint8 a) {
        //...
    }
    function anotherOldFunction() constant returns (bool) {
        //...
    }
    // ...
}
```

--------------------------------

### Solidity Custom Type with Operator Overloading

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

This Solidity example defines a custom fixed-point number type 'UFixed16x2' and overloads the '+' and '/' operators using a library. It demonstrates how to wrap and unwrap uint16 values to create the custom type and includes error handling for division overflow.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.19;

type UFixed16x2 is uint16;

using {
    add as +,
    div as /
} for UFixed16x2 global;

uint32 constant SCALE = 100;

function add(UFixed16x2 a, UFixed16x2 b) pure returns (UFixed16x2) {
    return UFixed16x2.wrap(UFixed16x2.unwrap(a) + UFixed16x2.unwrap(b));
}

function div(UFixed16x2 a, UFixed16x2 b) pure returns (UFixed16x2) {
    uint32 a32 = UFixed16x2.unwrap(a);
    uint32 b32 = UFixed16x2.unwrap(b);
    uint32 result32 = a32 * SCALE / b32;
    require(result32 <= type(uint16).max, "Divide overflow");
    return UFixed16x2.wrap(uint16(a32 * SCALE / b32));
}

contract Math {
    function avg(UFixed16x2 a, UFixed16x2 b) public pure returns (UFixed16x2) {
        return (a + b) / UFixed16x2.wrap(200);
    }
}
```

--------------------------------

### Solidity Fallback Function Example (No Payable)

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Demonstrates a basic fallback function in Solidity that does not accept Ether. This function is triggered for calls to the contract when no other matching function is found. It modifies state variable 'x' but will reject Ether transfers.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.2 <0.9.0;

contract Test {
    uint x;
    // This function is called for all messages sent to
    // this contract (there is no other function).
    // Sending Ether to this contract will cause an exception,
    // because the fallback function does not have the `payable`
    // modifier.
    fallback() external { x = 1; }
}
```

--------------------------------

### Optimize Array Summation using Inline Assembly in Solidity

Source: https://docs.soliditylang.org/en/v0.8.30/assembly

This example contrasts a Solidity function for summing array elements with two inline assembly versions. The first assembly function `sumAsm` demonstrates optimizing array access by directly calculating memory offsets, avoiding bounds checks. The `sumPureAsm` function further optimizes by performing the entire loop and summation within a single assembly block, leading to more efficient gas usage.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;


library VectorSum {
    // This function is less efficient because the optimizer currently fails to
    // remove the bounds checks in array access.
    function sumSolidity(uint[] memory data) public pure returns (uint sum) {
        for (uint i = 0; i < data.length; ++i)
            sum += data[i];
    }

    // We know that we only access the array in bounds, so we can avoid the check.
    // 0x20 needs to be added to an array because the first slot contains the
    // array length.
    function sumAsm(uint[] memory data) public pure returns (uint sum) {
        for (uint i = 0; i < data.length; ++i) {
            assembly {
                sum := add(sum, mload(add(add(data, 0x20), mul(i, 0x20))))
            }
        }
    }

    // Same as above, but accomplish the entire code within inline assembly.
    function sumPureAsm(uint[] memory data) public pure returns (uint sum) {
        assembly {
            // Load the length (first 32 bytes)
            let len := mload(data)

            // Skip over the length field.
            //
            // Keep temporary variable so it can be incremented in place.
            //
            // NOTE: incrementing data would result in an unusable
            //       data variable after this assembly block
            let dataElementLocation := add(data, 0x20)

            // Iterate until the bound is not met.
            for
                { let end := add(dataElementLocation, mul(len, 0x20)) }
                lt(dataElementLocation, end)
                { dataElementLocation := add(dataElementLocation, 0x20) }
            {
                sum := add(sum, mload(dataElementLocation))
            }
        }
    }
}
```

--------------------------------

### Solidity Output Selection Configuration

Source: https://docs.soliditylang.org/en/v0.8.30/using-the-compiler

Defines which compilation artifacts to generate, including AST, ABI, bytecode, source maps, and more, for specific files and contracts.

```json
{
  "outputSelection": {
    "*": {
      "*": [
        "metadata", "evm.bytecode", 
        "evm.bytecode.sourceMap"
      ],
      "": [
        "ast"
      ]
    },
    "def": {
      "MyContract": [ "abi", "evm.bytecode.opcodes" ]
    }
  }
}
```

--------------------------------

### Solidity Blind Auction Contract Structure and Logic

Source: https://docs.soliditylang.org/en/v0.8.30/solidity-by-example

This snippet defines the `BlindAuction` smart contract in Solidity. It includes the contract's state variables, structs, events, custom errors, modifiers, constructor, and core functions for bidding (`bid`) and revealing bids (`reveal`). The contract manages deposits, tracks the highest bid, and handles refunds.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.4;
contract BlindAuction {
    struct Bid {
        bytes32 blindedBid;
        uint deposit;
    }

    address payable public beneficiary;
    uint public biddingEnd;
    uint public revealEnd;
    bool public ended;

    mapping(address => Bid[]) public bids;

    address public highestBidder;
    uint public highestBid;

    // Allowed withdrawals of previous bids
    mapping(address => uint) pendingReturns;

    event AuctionEnded(address winner, uint highestBid);

    // Errors that describe failures.

    /// The function has been called too early.
    /// Try again at `time`.
    error TooEarly(uint time);
    /// The function has been called too late.
    /// It cannot be called after `time`.
    error TooLate(uint time);
    /// The function auctionEnd has already been called.
    error AuctionEndAlreadyCalled();

    // Modifiers are a convenient way to validate inputs to
    // functions. `onlyBefore` is applied to `bid` below:
    // The new function body is the modifier's body where
    // `_` is replaced by the old function body.
    modifier onlyBefore(uint time) {
        if (block.timestamp >= time) revert TooLate(time);
        _;
    }
    modifier onlyAfter(uint time) {
        if (block.timestamp <= time) revert TooEarly(time);
        _;
    }

    constructor(
        uint biddingTime,
        uint revealTime,
        address payable beneficiaryAddress
    ) {
        beneficiary = beneficiaryAddress;
        biddingEnd = block.timestamp + biddingTime;
        revealEnd = biddingEnd + revealTime;
    }

    /// Place a blinded bid with `blindedBid` = 
    /// keccak256(abi.encodePacked(value, fake, secret)).
    /// The sent ether is only refunded if the bid is correctly
    /// revealed in the revealing phase. The bid is valid if the
    /// ether sent together with the bid is at least "value" and
    /// "fake" is not true. Setting "fake" to true and sending
    /// not the exact amount are ways to hide the real bid but
    /// still make the required deposit. The same address can
    /// place multiple bids.
    function bid(
        bytes32 blindedBid
    )
        external
        payable
        onlyBefore(biddingEnd)
    {
        bids[msg.sender].push(Bid({
            blindedBid: blindedBid,
            deposit: msg.value
        }));
    }

    /// Reveal your blinded bids. You will get a refund for all
    /// correctly blinded invalid bids and for all bids except for
    /// the totally highest.
    function reveal(
        uint[] calldata values,
        bool[] calldata fakes,
        bytes32[] calldata secrets
    )
        external
        onlyAfter(biddingEnd)
        onlyBefore(revealEnd)
    {
        uint length = bids[msg.sender].length;
        require(values.length == length);
        require(fakes.length == length);
        require(secrets.length == length);

        uint refund;
        for (uint i = 0; i < length; i++) {
            Bid storage bidToCheck = bids[msg.sender][i];
            (uint value, bool fake, bytes32 secret) = 
                    (values[i], fakes[i], secrets[i]);
            if (bidToCheck.blindedBid != keccak256(abi.encodePacked(value, fake, secret))) {
                // Bid was not actually revealed.
                // Do not refund deposit.
                continue;
            }
            refund += bidToCheck.deposit;
            if (!fake && bidToCheck.deposit >= value) {

```

--------------------------------

### Memory-Safe Assembly: Using Free Memory Pointer (Solidity)

Source: https://docs.soliditylang.org/en/v0.8.30/assembly

This Solidity inline assembly example is memory-safe. It safely uses memory beyond the current free memory pointer for operations like `returndatacopy` and `revert`.

```solidity
assembly ("memory-safe") {
  let p := mload(0x40)
  returndatacopy(p, 0, returndatasize())
  revert(p, returndatasize())
}
```

--------------------------------

### Solidity Storage Layout Example

Source: https://docs.soliditylang.org/en/v0.8.30/internals/layout_in_storage

This JSON object represents the storage layout for a Solidity contract. It details each variable's contract, label, storage slot, offset, and type. It also includes a 'types' section describing the encoding and size of each data type used in the contract.

```json
{
  "storage": [
    {
      "astId": 15,
      "contract": "fileA:A",
      "label": "x",
      "offset": 0,
      "slot": "0",
      "type": "t_uint256"
    },
    {
      "astId": 19,
      "contract": "fileA:A",
      "label": "w",
      "offset": 0,
      "slot": "1",
      "type": "t_uint256"
    },
    {
      "astId": 24,
      "contract": "fileA:A",
      "label": "s",
      "offset": 0,
      "slot": "2",
      "type": "t_struct(S)13_storage"
    },
    {
      "astId": 26,
      "contract": "fileA:A",
      "label": "addr",
      "offset": 0,
      "slot": "6",
      "type": "t_address"
    },
    {
      "astId": 34,
      "contract": "fileA:A",
      "label": "map",
      "offset": 0,
      "slot": "7",
      "type": "t_mapping(t_uint256,t_mapping(t_address,t_bool))"
    },
    {
      "astId": 37,
      "contract": "fileA:A",
      "label": "array",
      "offset": 0,
      "slot": "8",
      "type": "t_array(t_uint256)dyn_storage"
    },
    {
      "astId": 39,
      "contract": "fileA:A",
      "label": "s1",
      "offset": 0,
      "slot": "9",
      "type": "t_string_storage"
    },
    {
      "astId": 41,
      "contract": "fileA:A",
      "label": "b1",
      "offset": 0,
      "slot": "10",
      "type": "t_bytes_storage"
    }
  ],
  "types": {
    "t_address": {
      "encoding": "inplace",
      "label": "address",
      "numberOfBytes": "20"
    },
    "t_array(t_uint256)2_storage": {
      "base": "t_uint256",
      "encoding": "inplace",
      "label": "uint256[2]",
      "numberOfBytes": "64"
    },
    "t_array(t_uint256)dyn_storage": {
      "base": "t_uint256",
      "encoding": "dynamic_array",
      "label": "uint256[]",
      "numberOfBytes": "32"
    },
    "t_bool": {
      "encoding": "inplace",
      "label": "bool",
      "numberOfBytes": "1"
    },
    "t_bytes_storage": {
      "encoding": "bytes",
      "label": "bytes",
      "numberOfBytes": "32"
    },
    "t_mapping(t_address,t_bool)": {
      "encoding": "mapping",
      "key": "t_address",
      "label": "mapping(address => bool)",
      "numberOfBytes": "32",
      "value": "t_bool"
    },
    "t_mapping(t_uint256,t_mapping(t_address,t_bool))": {
      "encoding": "mapping",
      "key": "t_uint256",
      "label": "mapping(uint256 => mapping(address => bool))",
      "numberOfBytes": "32",
      "value": "t_mapping(t_address,t_bool)"
    },
    "t_string_storage": {
      "encoding": "bytes",
      "label": "string",
      "numberOfBytes": "32"
    },
    "t_struct(S)13_storage": {
      "encoding": "inplace",
      "label": "struct A.S",
      "members": [
        {
          "astId": 3,
          "contract": "fileA:A",
          "label": "a",
          "offset": 0,
          "slot": "0",
          "type": "t_uint128"
        },
        {
          "astId": 5,
          "contract": "fileA:A",
          "label": "b",
          "offset": 16,
          "slot": "0",
          "type": "t_uint128"
        },
        {
          "astId": 9,
          "contract": "fileA:A",
          "label": "staticArray",
          "offset": 0,
          "slot": "1",
          "type": "t_array(t_uint256)2_storage"
        },
        {
          "astId": 12,
          "contract": "fileA:A",
          "label": "dynArray",
          "offset": 0,
          "slot": "3",
          "type": "t_array(t_uint256)dyn_storage"
        }
      ],
      "numberOfBytes": "128"
    },
    "t_uint128": {
      "encoding": "inplace",
      "label": "uint128",
      "numberOfBytes": "16"
    },
    "t_uint256": {
      "encoding": "inplace",
      "label": "uint256",
      "numberOfBytes": "32"
    }
  }
}
```

--------------------------------

### Solidity IterableMapping Library and User Contract Example

Source: https://docs.soliditylang.org/en/v0.8.30/types

This snippet provides a complete implementation of an IterableMapping library in Solidity, including functions for insertion, removal, containment checks, and iteration. It also shows a 'User' contract that utilizes this library to manage data and compute sums.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.8;

struct IndexValue { uint keyIndex; uint value; }
struct KeyFlag { uint key; bool deleted; }

struct itmap {
    mapping(uint => IndexValue) data;
    KeyFlag[] keys;
    uint size;
}

type Iterator is uint;

library IterableMapping {
    function insert(itmap storage self, uint key, uint value) internal returns (bool replaced) {
        uint keyIndex = self.data[key].keyIndex;
        self.data[key].value = value;
        if (keyIndex > 0)
            return true;
        else {
            keyIndex = self.keys.length;
            self.keys.push();
            self.data[key].keyIndex = keyIndex + 1;
            self.keys[keyIndex].key = key;
            self.size++;
            return false;
        }
    }

    function remove(itmap storage self, uint key) internal returns (bool success) {
        uint keyIndex = self.data[key].keyIndex;
        if (keyIndex == 0)
            return false;
        delete self.data[key];
        self.keys[keyIndex - 1].deleted = true;
        self.size --;
    }

    function contains(itmap storage self, uint key) internal view returns (bool) {
        return self.data[key].keyIndex > 0;
    }

    function iterateStart(itmap storage self) internal view returns (Iterator) {
        return iteratorSkipDeleted(self, 0);
    }

    function iterateValid(itmap storage self, Iterator iterator) internal view returns (bool) {
        return Iterator.unwrap(iterator) < self.keys.length;
    }

    function iterateNext(itmap storage self, Iterator iterator) internal view returns (Iterator) {
        return iteratorSkipDeleted(self, Iterator.unwrap(iterator) + 1);
    }

    function iterateGet(itmap storage self, Iterator iterator) internal view returns (uint key, uint value) {
        uint keyIndex = Iterator.unwrap(iterator);
        key = self.keys[keyIndex].key;
        value = self.data[key].value;
    }

    function iteratorSkipDeleted(itmap storage self, uint keyIndex) private view returns (Iterator) {
        while (keyIndex < self.keys.length && self.keys[keyIndex].deleted)
            keyIndex++;
        return Iterator.wrap(keyIndex);
    }
}

// How to use it
contract User {
    // Just a struct holding our data.
    itmap data;
    // Apply library functions to the data type.
    using IterableMapping for itmap;

    // Insert something
    function insert(uint k, uint v) public returns (uint size) {
        // This calls IterableMapping.insert(data, k, v)
        data.insert(k, v);
        // We can still access members of the struct,
        // but we should take care not to mess with them.
        return data.size;
    }

    // Computes the sum of all stored data.
    function sum() public view returns (uint s) {
        for (
            Iterator i = data.iterateStart();
            data.iterateValid(i);
            i = data.iterateNext(i)
        ) {
            (, uint value) = data.iterateGet(i);
            s += value;
        }
    }
}
```

--------------------------------

### Execute Solidity Fuzzer with Test Cases

Source: https://docs.soliditylang.org/en/v0.8.30/contributing

Command to run the afl-fuzz tool with specified memory limit, input test cases, output directory, and the target binary 'solfuzzer'.

```bash
afl-fuzz -m 60 -i /tmp/test_cases -o /tmp/fuzzer_reports -- /path/to/solfuzzer
```

--------------------------------

### Solidity Transient Storage Layout Example

Source: https://docs.soliditylang.org/en/v0.8.30/internals/layout_in_storage

This JSON object details the transient storage layout for a Solidity contract. It lists variables stored temporarily, including their contract, label, storage slot, offset, and type, along with descriptions of the data types used.

```json
{
  "storage": [
    {
      "astId": 17,
      "contract": "fileA:A",
      "label": "y",
      "offset": 0,
      "slot": "0",
      "type": "t_uint256"
    },
    {
      "astId": 21,
      "contract": "fileA:A",
      "label": "z",
      "offset": 0,
      "slot": "1",
      "type": "t_uint256"
    },
    {
      "astId": 28,
      "contract": "fileA:A",
      "label": "taddr",
      "offset": 0,
      "slot": "2",
      "type": "t_address"
    }
  ],
  "types": {
    "t_address": {
      "encoding": "inplace",
      "label": "address",
      "numberOfBytes": "20"
    },
    "t_uint256": {
      "encoding": "inplace",
      "label": "uint256",
      "numberOfBytes": "32"
    }
  }
}
```

--------------------------------

### Solidity: Calldata Array Slicing

Source: https://docs.soliditylang.org/en/v0.8.30/060-breaking-changes

Enables the use of array slices for `calldata` arrays, facilitating low-level decoding of function call payloads. Example: `abi.decode(msg.data[4:], (uint, uint))`.

```Solidity
pragma solidity ^0.6.0;

contract CalldataDecoder {
    function decodePayload(bytes memory calldataPayload) public pure {
        // Example: Assuming calldataPayload is function signature (4 bytes) + arguments
        // Decode two uints from the payload after the selector
        (uint arg1, uint arg2) = abi.decode(calldataPayload[4:], (uint, uint));
        // Use arg1 and arg2
    }
}
```

--------------------------------

### Solidity AST Import

Source: https://docs.soliditylang.org/en/v0.8.30/using-the-compiler

Details the structure for importing Solidity Abstract Syntax Trees (ASTs). This is an experimental feature and requires the `language` to be set to `SolidityAST`.

```json
{
  "ast": { ... } 
}
```

--------------------------------

### Solidity Library Linking Configuration

Source: https://docs.soliditylang.org/en/v0.8.30/using-the-compiler

Specifies library addresses for linking, organized by source file. An empty string key indicates global level linking.

```json
{
  "libraries": {
    "myFile.sol": {
      "MyLib": "0x123123..."
    }
  }
}
```

--------------------------------

### Solidity Contract Receiving Ether

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

An example of a Solidity contract named 'Sink' that implements the `receive` function to accept Ether transfers. It emits an event upon receiving Ether, logging the sender's address and the amount received. This contract is designed to hold Ether indefinitely.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

// This contract keeps all Ether sent to it with no way
// to get it back.
contract Sink {
    event Received(address, uint);
    receive() external payable {
        emit Received(msg.sender, msg.value);
    }
}

```

--------------------------------

### Solidity Array Element Getter and Full Array Retrieval

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Shows how Solidity getters access individual array elements via an index. It also provides an example of a custom function to return the entire array, as direct external access to a full array is gas-intensive.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract arrayExample {
    // public state variable
    uint[] public myArray;

    // Getter function generated by the compiler
    /*
    function myArray(uint i) public view returns (uint) {
        return myArray[i];
    }
    */

    // function that returns entire array
    function getArray() public view returns (uint[] memory) {
        return myArray;
    }
}
```

--------------------------------

### Activate Optimizer for Bytecode and Yul IR

Source: https://docs.soliditylang.org/en/v0.8.30/internals/optimizer

Activates the opcode-based optimizer for generated bytecode and the Yul optimizer for internal Yul code, such as for ABI coder v2. It also demonstrates how to produce an optimized Yul IR or use a strict assembly mode.

```bash
solc --optimize
solc --ir-optimized --optimize
solc --strict-assembly --optimize
```

--------------------------------

### Solidity: onlyOwner Modifier Example

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Demonstrates the 'onlyOwner' modifier to restrict function access to the contract owner. It checks if the message sender is the owner and throws an error otherwise. The '_;' placeholder inserts the function's body.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.1 <0.9.0;

contract owned {
    constructor() { owner = payable(msg.sender); }
    address payable owner;

    // This contract only defines a modifier but does not use
    // it: it will be used in derived contracts.
    // The function body is inserted where the special symbol
    // `_;` in the definition of a modifier appears.
    // This means that if the owner calls this function, the
    // function is executed and otherwise, an exception is
    // thrown.
    modifier onlyOwner {
        require(
            msg.sender == owner,
            "Only owner can call this function."
        );
        _;
    }
}

contract Register is owned {
    // This contract inherits the `onlyOwner` modifier from
    // the `owned` contract. As a result, calls to `changePrice` will
    // only take effect if they are made by the stored owner.
    function changePrice(uint price_) public onlyOwner {
        price = price_; // Assuming 'price' is a state variable in a derived contract
    }
}
```

--------------------------------

### Solidity Ternary Operator Example

Source: https://docs.soliditylang.org/en/v0.8.30/types

Demonstrates the use of the ternary operator in Solidity for conditional expression evaluation. It highlights how the operator's result type is determined and potential issues like arithmetic overflow when operands have specific types.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

contract TernaryExample {
    function conditionalAdd(uint a, bool condition) public pure returns (uint) {
        // If condition is true, add 1, otherwise add 0.
        // Note: The type of the result (uint8) can cause overflow if not handled carefully.
        // For example: 255 + (true ? 1 : 0) would revert.
        uint result = a + (condition ? 1 : 0);
        return result;
    }

    function conditionalDecimal(bool condition) public pure returns (string memory) {
        // Demonstrates type issues with rational numbers and integers.
        // 1.5 + 1.5 is valid (unlimited precision).
        // 1.5 + (true ? 1 : 2.5) is invalid due to conversion to integer.
        if (condition) {
            return "Operation valid with same types.";
        } else {
            return "Operation invalid with mixed types.";
        }
    }
}
```

--------------------------------

### Run Soltest on Windows (Git Bash)

Source: https://docs.soliditylang.org/en/v0.8.30/contributing

Command to run the Soltest executable on Windows using Git Bash, with SMT tests disabled.

```shell
./build/test/Release/soltest.exe -- --no-smt
```

--------------------------------

### Solidity Contract - Old Version (pre-0.5.0)

Source: https://docs.soliditylang.org/en/v0.8.30/050-breaking-changes

An example of a Solidity contract written for versions prior to 0.5.0. It includes features and syntax that are no longer supported or have changed in later versions, such as implicit function mutability and visibility, and the use of 'throw'.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.4.25;
// This will not compile after 0.5.0

contract OtherContract {
    uint x;
    function f(uint y) external {
        x = y;
    }
    function() payable external {}
}

contract Old {
    OtherContract other;
    uint myNumber;

    // Function mutability not provided, not an error.
    function someInteger() internal returns (uint) { return 2; }

    // Function visibility not provided, not an error.
    // Function mutability not provided, not an error.
    function f(uint x) returns (bytes) {
        // Var is fine in this version.
        var z = someInteger();
        x += z;
        // Throw is fine in this version.
        if (x > 100)
            throw;
        bytes memory b = new bytes(x);
        y = -3 >> 1;
        // y == -1 (wrong, should be -2)
        do {
            x += 1;
            if (x > 10) continue;
            // 'Continue' causes an infinite loop.
        } while (x < 11);
        // Call returns only a Bool.
        bool success = address(other).call("f");
        if (!success)
            revert();
        else {
            // Local variables could be declared after their use.
            int y;
        }
        return b;
    }

    // No need for an explicit data location for 'arr'
    function g(uint[] arr, bytes8 x, OtherContract otherContract) public {
        otherContract.transfer(1 ether);

        // Since uint32 (4 bytes) is smaller than bytes8 (8 bytes),
        // the first 4 bytes of x will be lost. This might lead to
        // unexpected behavior since bytesX are right padded.
        uint32 y = uint32(x);
        myNumber += y + msg.value;
    }
}

```

--------------------------------

### Solidity: Multi-step explicit type conversions

Source: https://docs.soliditylang.org/en/v0.8.30/080-breaking-changes

To perform multiple changes in sign, width, or type-category during explicit conversions, use multiple conversion steps. For example, converting from `int8` to `uint16` requires intermediate conversions.

```Solidity
uint16(int8)
```

```Solidity
uint16(uint8(int8))
```

```Solidity
uint16(int16(int8))
```

--------------------------------

### Solidity Auction Contract Logic

Source: https://docs.soliditylang.org/en/v0.8.30/solidity-by-example

Demonstrates the core logic of an auction contract, including conditional checks before state changes and ether transfer. It reverts if the auction has not ended or if the end function has already been called. It emits an 'AuctionEnded' event upon successful execution.

```Solidity
// effects (ether payout) to be performed multiple times.
        // If functions called internally include interaction with external
        // contracts, they also have to be considered interaction with
        // external contracts.

        // 1. Conditions
        if (block.timestamp < auctionEndTime)
            revert AuctionNotYetEnded();
        if (ended)
            revert AuctionEndAlreadyCalled();

        // 2. Effects
        ended = true;
        emit AuctionEnded(highestBidder, highestBid);

        // 3. Interaction
        beneficiary.transfer(highestBid);
    }
}
```

--------------------------------

### Solidity Compiler Optimizer Options

Source: https://docs.soliditylang.org/en/v0.8.30/using-the-compiler

Explains how to use the optimizer flag with solc to improve contract performance. It details the `--optimize` flag and the `--optimize-runs` parameter, which allows customization of optimization based on expected contract usage.

```bash
solc --optimize --bin sourceFile.sol
solc --optimize --optimize-runs=1 --bin sourceFile.sol
```

--------------------------------

### Solidity Storage Layout - State Variable Example

Source: https://docs.soliditylang.org/en/v0.8.30/internals/layout_in_storage

Describes the structure of an entry in the 'storage' array of the JSON output. Each entry represents a state variable, detailing its AST ID, contract name, label (name), offset within the slot, storage slot number, and type identifier.

```json
{
    "astId": 2,
    "contract": "fileA:A",
    "label": "x",
    "offset": 0,
    "slot": "0",
    "type": "t_uint256"
}
```

--------------------------------

### Build and Run Solidity Fuzzer

Source: https://docs.soliditylang.org/en/v0.8.30/contributing

Commands to clean, build, and execute the Solidity fuzzer ('solfuzzer') using AFL. It specifies the C/C++ compilers to use and the memory limit for the fuzzer.

```bash
make clean
cmake .. -DCMAKE_C_COMPILER=path/to/afl-clang -DCMAKE_CXX_COMPILER=path/to/afl-clang++
make solfuzzer
```

--------------------------------

### Compiler Settings - Optimizer

Source: https://docs.soliditylang.org/en/v0.8.30/using-the-compiler

Defines optimizer settings for the Solidity compiler. This includes enabling the optimizer, setting the number of runs for optimization, and configuring specific optimizer components.

```json
{
  "optimizer": {
    "enabled": true,
    "runs": 200,
    "details": {
      "peephole": true
    }
  }
}
```

--------------------------------

### Solidity: Using Contract Members and Selectors

Source: https://docs.soliditylang.org/en/v0.8.30/types

Demonstrates how to access contract members like address and selector. It shows the use of `assert` for preconditions and how to make external calls with specified gas and value.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.4 <0.9.0;

contract Example {
    function f() public payable returns (bytes4) {
        assert(this.f.address == address(this));
        return this.f.selector;
    }

    function g() public {
        this.f{gas: 10, value: 800}();
    }
}

```

--------------------------------

### Address Literals in Solidity

Source: https://docs.soliditylang.org/en/v0.8.30/types

Shows examples of valid hexadecimal address literals in Solidity, including those that pass the EIP-55 checksum test. It also mentions that literals failing the checksum test can cause errors unless padded with zeros.

```Solidity
pragma solidity ^0.8.30;

contract AddressLiterals {
    address validAddress = 0xdCad3a6d3569DF655070DEd06cb7A1b2Ccd1D3AF;
    address anotherValidAddress = 0x787192fc7189886107a999610337c784204c546d;
    // address invalidAddress = 0xdCad3a6d3569DF655070DEd06cb7A1b2Ccd1D3A5; // This would likely cause a compilation error without padding
}
```

--------------------------------

### Wei to Ether Conversion in Solidity

Source: https://docs.soliditylang.org/en/v0.8.30/introduction-to-smart-contracts

Demonstrates the conversion between Wei and Ether, the fundamental units of currency on the Ethereum network. 1 Ether is equivalent to 10^18 Wei.

```Solidity
uint256 public constant etherInWei = 10**18;

function convertToEther(uint256 weiAmount) public pure returns (uint256) {
    return weiAmount / etherInWei;
}

function convertToWei(uint256 etherAmount) public pure returns (uint256) {
    return etherAmount * etherInWei;
}
```

--------------------------------

### Solidity: noReentrancy Modifier Example

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Provides a 'noReentrancy' modifier to prevent reentrant calls. It uses a boolean flag 'locked' to ensure a function's execution is not interrupted by recursive calls from within itself, protecting against reentrancy attacks.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.1 <0.9.0;

contract Mutex {
    bool locked;
    modifier noReentrancy() {
        require(
            !locked,
            "Reentrant call."
        );
        locked = true;
        _;
        locked = false;
    }

    /// This function is protected by a mutex, which means that
    /// reentrant calls from within `msg.sender.call` cannot call `f` again.
    /// The `return 7` statement assigns 7 to the return value but still
    /// executes the statement `locked = false` in the modifier.
    function f() public noReentrancy returns (uint) {
        (bool success,) = msg.sender.call("");
        require(success);
        return 7;
    }
}
```

--------------------------------

### Run All Solidity Tests

Source: https://docs.soliditylang.org/en/v0.8.30/contributing

Executes most Solidity tests, including those from the Boost C++ Test Framework, command-line tests, and compilation tests. It automatically discovers the evmone location for semantic tests.

```shell
./scripts/tests.sh
```

--------------------------------

### Use Pre-0.5.0 Contract via Interface in New Contract

Source: https://docs.soliditylang.org/en/v0.8.30/050-breaking-changes

This example shows a new Solidity contract (v0.5.0+) interacting with a pre-0.5.0 contract using a defined interface. The `NewContract`'s `doSomething` function calls functions from the `OldContract` interface, demonstrating successful interoperability.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.5.0 <0.9.0;

interface OldContract {
    function someOldFunction(uint8 a) external;
    function anotherOldFunction() external returns (bool);
}

contract NewContract {
    function doSomething(OldContract a) public returns (bool) {
        a.someOldFunction(0x42);
        return a.anotherOldFunction();
    }
}
```

--------------------------------

### Solidity: Delegate Vote Function

Source: https://docs.soliditylang.org/en/v0.8.30/solidity-by-example

Enables a voter to delegate their vote to another address. It prevents self-delegation and delegation loops, and ensures the recipient has voting rights. If the delegate has already voted, the sender's weight is immediately added to the delegate's vote count.

```solidity
/// Delegate your vote to the voter `to`.
function delegate(address to) external {
    // assigns reference
    Voter storage sender = voters[msg.sender];
    require(sender.weight != 0, "You have no right to vote");
    require(!sender.voted, "You already voted.");

    require(to != msg.sender, "Self-delegation is disallowed.");

    // Forward the delegation as long as
    // `to` also delegated.
    // In general, such loops are very dangerous, 
    // because if they run too long, they might
    // need more gas than is available in a block.
    // In this case, the delegation will not be executed,
    // but in other situations, such loops might
    // cause a contract to get "stuck" completely.
    while (voters[to].delegate != address(0)) {
        to = voters[to].delegate;

        // We found a loop in the delegation, not allowed.
        require(to != msg.sender, "Found loop in delegation.");
    }

    Voter storage delegate_ = voters[to];

    // Voters cannot delegate to accounts that cannot vote.
    require(delegate_.weight >= 1);

    // Since `sender` is a reference, this
    // modifies `voters[msg.sender]`.
    sender.voted = true;
    sender.delegate = to;

    if (delegate_.voted) {
        // If the delegate already voted,
        // directly add to the number of votes
        proposals[delegate_.vote].voteCount += sender.weight;

```

--------------------------------

### Unsigned Integer Cleanup Example (Solidity)

Source: https://docs.soliditylang.org/en/v0.8.30/internals/variable_cleanup

Illustrates the cleaning process for an unsigned 8-bit integer (uint8). Invalid values, which have higher bits set to zero, are shown being cleaned by zeroing out these higher bits, resulting in a valid representation.

```solidity
0000...0000 0000 0000
0000...0000 0000 0001
0000...0000 0000 0010
....
0000...0000 1111 1111

0101...1101 0010 1010   invalid value
0000...0000 0010 1010   cleaned value
```

--------------------------------

### Solidity Debugging and Metadata Configuration

Source: https://docs.soliditylang.org/en/v0.8.30/using-the-compiler

Configures debugging information to include location and snippet, and sets metadata appending, literal content usage, and bytecode hash method.

```json
{
  "debugInfo": ["location", "snippet"],
  "metadata": {
    "appendCBOR": true,
    "useLiteralContent": true,
    "bytecodeHash": "ipfs"
  }
}
```

--------------------------------

### Solidity Max Element Assertion

Source: https://docs.soliditylang.org/en/v0.8.30/smtchecker

This Solidity contract finds the maximum element in an array and uses an 'assert' statement to verify that the found maximum is greater than or equal to every element in the array. This example includes checks for loop overflow.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.0;

contract Max {
    function max(uint[] memory a) public pure returns (uint) {
        uint m = 0;
        for (uint i = 0; i < a.length; ++i)
            if (a[i] > m)
                m = a[i];

        for (uint i = 0; i < a.length; ++i)
            assert(m >= a[i]);

        return m;
    }
}

```

--------------------------------

### Solidity abi.encodePacked() Collision Example

Source: https://docs.soliditylang.org/en/v0.8.30/abi-spec

Shows a potential security vulnerability in Solidity's packed encoding related to hash collisions when using keccak256(abi.encodePacked(a, b)) with dynamic types. It demonstrates how data can be rearranged between dynamic types leading to the same hash.

```Solidity
abi.encodePacked("a", "bc") == abi.encodePacked("ab", "c")
```

--------------------------------

### Solidity Overloading with ABI Conflict Example

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Illustrates a scenario in Solidity where function overloading based on different types (e.g., custom contract type B vs. address) can lead to compilation errors due to ABI considerations, as both might resolve to the same external type.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

// This will not compile
contract A {
    function f(B value) public pure returns (B out) {
        out = value;
    }

    function f(address value) public pure returns (address out) {
        out = value;
    }
}

contract B {
}

```

--------------------------------

### Execute Solidity Command-line Tests with Filtering

Source: https://docs.soliditylang.org/en/v0.8.30/contributing

This command executes Solidity's command-line tests. It allows specifying patterns to include or exclude specific tests and setting the build directory for the compiler binary.

```bash
export SOLIDITY_BUILD_DIR=~/solidity/build/
test/cmdlineTests.sh "standard_*" "*_yul_*" --exclude "standard_yul_*"

```

--------------------------------

### Querying Contract Code and Hash

Source: https://docs.soliditylang.org/en/v0.8.30/types

Demonstrates how to retrieve the EVM bytecode of a smart contract using `.code` and its Keccak-256 hash using `.codehash`. It also notes the cost efficiency of `.codehash` over manual hashing and potential return values for empty or non-existent accounts as per EIP-1052.

```Solidity
pragma solidity ^0.8.30;

contract ContractQuerier {
    function getContractCode(address addr) public view returns (bytes memory) {
        return addr.code;
    }

    function getContractCodeHash(address addr) public view returns (bytes32) {
        return addr.codehash;
    }
}
```

--------------------------------

### Solidity Assembly: Allocate Memory

Source: https://docs.soliditylang.org/en/v0.8.30/assembly

An assembly snippet for allocating memory in Solidity. It uses the free memory pointer to find available space and updates the pointer after allocation. This function takes the desired length as input and returns the starting position of the allocated memory.

```assembly
function allocate(length) -> pos {
  pos := mload(0x40)
  mstore(0x40, add(pos, length))
}
```

--------------------------------

### Solidity abi.encodePacked() Example

Source: https://docs.soliditylang.org/en/v0.8.30/abi-spec

Demonstrates the non-standard packed encoding of various Solidity types using abi.encodePacked(). Types shorter than 32 bytes are concatenated directly without padding. Dynamic types are encoded in-place without length. Array elements are padded. Structs and nested arrays are not supported.

```Solidity
int16(-1), bytes1(0x42), uint16(0x03), string("Hello, world!")
```

--------------------------------

### Solidity Contract - New Version (0.5.0+)

Source: https://docs.soliditylang.org/en/v0.8.30/050-breaking-changes

An example of a Solidity contract updated for version 0.5.0 and later. It demonstrates required syntax changes, including explicit function mutability and visibility, the use of 'require' instead of 'throw', updated call return types, and explicit data location specifiers.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.5.0;
// This will not compile after 0.6.0

contract OtherContract {
    uint x;
    function f(uint y) external {
        x = y;
    }
    function() payable external {}
}

contract New {
    OtherContract other;
    uint myNumber;

    // Function mutability must be specified.
    function someInteger() internal pure returns (uint) { return 2; }

    // Function visibility must be specified.
    // Function mutability must be specified.
    function f(uint x) public returns (bytes memory) {
        // The type must now be explicitly given.
        uint z = someInteger();
        x += z;
        // Throw is now disallowed.
        require(x <= 100);
        int y = -3 >> 1;
        require(y == -2);
        do {
            x += 1;
            if (x > 10) continue;
            // 'Continue' jumps to the condition below.
        } while (x < 11);

        // Call returns (bool, bytes).
        // Data location must be specified.
        (bool success, bytes memory data) = address(other).call("f");
        if (!success)
            revert();
        return data;
    }

    using AddressMakePayable for address;
    // Data location for 'arr' must be specified
    function g(uint[] memory /* arr */, bytes8 x, OtherContract otherContract, address unknownContract) public payable {
        // 'otherContract.transfer' is not provided.
        // Since the code of 'OtherContract' is known and has the fallback
        // function, address(otherContract) has type 'address payable'.
        address(otherContract).transfer(1 ether);

        // 'unknownContract.transfer' is not provided.
        // 'address(unknownContract).transfer' is not provided
        // since 'address(unknownContract)' is not 'address payable'.
        // If the function takes an 'address' which you want to send
        // funds to, you can convert it to 'address payable' via 'uint160'.
        // Note: This is not recommended and the explicit type
        // 'address payable' should be used whenever possible.
        // To increase clarity, we suggest the use of a library for
        // the conversion (provided after the contract in this example).
        address payable addr = unknownContract.makePayable();
        require(addr.send(1 ether));

        // Since uint32 (4 bytes) is smaller than bytes8 (8 bytes),
        // the conversion is not allowed.
        // We need to convert to a common size first:
        bytes4 x4 = bytes4(x); // Padding happens on the right
        uint32 y = uint32(x4); // Conversion is consistent
        // 'msg.value' cannot be used in a 'non-payable' function.
        // We need to make the function payable
        myNumber += y + msg.value;
    }
}

// We can define a library for explicitly converting ``address``
// to ``address payable`` as a workaround.
library AddressMakePayable {
    function makePayable(address x) internal pure returns (address payable) {
        return address(uint160(x));
    }
}

```

--------------------------------

### Solidity Abstract Contract with Constructor

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Demonstrates an abstract contract `A` with a constructor that initializes a state variable `a`, and a concrete contract `B` that inherits from `A` providing an initial value to the base constructor.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

abstract contract A {
    uint public a;

    constructor(uint a_) {
        a = a_;
    }
}

contract B is A(1) {
    constructor() {}
}

```

--------------------------------

### Type Conversion for `bytesX` and `uintY` (Solidity)

Source: https://docs.soliditylang.org/en/v0.8.30/050-breaking-changes

Solidity 0.8.30 disallows direct conversions between `bytesX` and `uintY` of different sizes due to padding issues. Sizes must be adjusted before conversion. For example, converting `bytes4` to `uint64` requires an intermediate conversion to `bytes8`.

```Solidity
pragma solidity ^0.8.30;

contract BytesUintConversion {
    function convertBytesToUint() public pure returns (uint64) {
        bytes4 data = 0x12345678;
        // Direct conversion disallowed
        // uint64 result = uint64(data);

        // Allowed: Adjust size first
        bytes8 paddedData = bytes8(data);
        uint64 result = uint64(paddedData);
        return result;
    }

    function convertUintToBytes() public pure returns (bytes4) {
        uint64 value = 0x0102030405060708;
        // Allowed: Convert through intermediate uint32 for opposite padding
        bytes4 result = bytes4(uint32(uint64(value)));
        return result;
    }
}
```

--------------------------------

### Solidity Contract Creation using 'new'

Source: https://docs.soliditylang.org/en/v0.8.30/control-structures

Illustrates creating new contracts in Solidity using the 'new' keyword. The full bytecode of the created contract must be known at compile time. It also shows how to send Ether during creation using the 'value' option and how creation failures are handled.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;
contract D {
    uint public x;
    constructor(uint a) payable {
        x = a;
    }
}

contract C {
    D d = new D(4); // will be executed as part of C's constructor

    function createD(uint arg) public {
        D newD = new D(arg);
        newD.x();
    }

    function createAndEndowD(uint arg, uint amount) public payable {
        // Send ether along with the creation
        D newD = new D{value: amount}(arg);
        newD.x();
    }
}
```

--------------------------------

### Solidity: Update .call() family for ABI encoding

Source: https://docs.soliditylang.org/en/v0.8.30/050-breaking-changes

Starting from Solidity v0.5.0, functions like .call(), .delegatecall(), and .staticcall() now accept only a single bytes argument and do not pad it. This change requires explicit ABI encoding for arguments. External calls with multiple arguments need to be converted to use abi.encodeWithSignature. Keccak256 operations also require explicit packing.

```Solidity
// Before v0.5.0
otherContract.call("f(uint256)", a, b);
keccak256(a, b, c);

// After v0.5.0
otherContract.call(abi.encodeWithSignature("f(uint256)", a, b));
keccak256(abi.encodePacked(a, b, c));
```

--------------------------------

### Solidity Compiler Import Remapping

Source: https://docs.soliditylang.org/en/v0.8.30/using-the-compiler

Illustrates how to configure import paths for the Solidity compiler using the prefix=path syntax. This allows the compiler to resolve imports from custom locations on the filesystem, including external repositories.

```bash
solc github.com/ethereum/dapp-bin/=/usr/local/lib/dapp-bin/ file.sol
```

--------------------------------

### Attaching File-Level Functions to a User-Defined Type in Solidity

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Demonstrates how to attach file-level functions (`insert`, `remove`, `contains`) to a user-defined struct type (`Data`) using the `using` directive. These functions are then available as member functions on instances of `Data` within the same scope. This example showcases a set-like behavior for the `Data` struct.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.13;

struct Data { mapping(uint => bool) flags; }
// Now we attach functions to the type.
// The attached functions can be used throughout the rest of the module.
// If you import the module, you have to
// repeat the using directive there, for example as
//   import "flags.sol" as Flags;
//   using {Flags.insert, Flags.remove, Flags.contains}
//     for Flags.Data;
using {insert, remove, contains} for Data;

function insert(Data storage self, uint value)
    returns (bool)
{
    if (self.flags[value])
        return false; // already there
    self.flags[value] = true;
    return true;
}

function remove(Data storage self, uint value)
    returns (bool)
{
    if (!self.flags[value])
        return false; // not there
    self.flags[value] = false;
    return true;
}

function contains(Data storage self, uint value)
    view
    returns (bool)
{
    return self.flags[value];
}


contract C {
    Data knownValues;

    function register(uint value) public {
        // Here, all variables of type Data have
        // corresponding member functions.
        // The following function call is identical to
        // `Set.insert(knownValues, value)`
    }
}

```

--------------------------------

### Solidity Subcurrency Contract

Source: https://docs.soliditylang.org/en/v0.8.30/introduction-to-smart-contracts

The main Solidity contract implementing a simple cryptocurrency. It allows the creator to mint coins and enables users to send coins to each other. It uses state variables, mappings for balances, and emits a 'Sent' event for transfers.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.26;

// This will only compile via IR
contract Coin {
    // The keyword "public" makes variables
    // accessible from other contracts
    address public minter;
    mapping(address => uint) public balances;

    // Events allow clients to react to specific
    // contract changes you declare
    event Sent(address from, address to, uint amount);

    // Constructor code is only run when the contract
    // is created
    constructor() {
        minter = msg.sender;
    }

    // Sends an amount of newly created coins to an address
    // Can only be called by the contract creator
    function mint(address receiver, uint amount) public {
        require(msg.sender == minter);
        balances[receiver] += amount;
    }

    // Errors allow you to provide information about
    // why an operation failed. They are returned
    // to the caller of the function.
    error InsufficientBalance(uint requested, uint available);

    // Sends an amount of existing coins
    // from any caller to an address
    function send(address receiver, uint amount) public {
        require(amount <= balances[msg.sender], InsufficientBalance(amount, balances[msg.sender]));
        balances[msg.sender] -= amount;
        balances[receiver] += amount;
        emit Sent(msg.sender, receiver, amount);
    }
}

```

--------------------------------

### Signed Integer Cleanup Example (Solidity)

Source: https://docs.soliditylang.org/en/v0.8.30/internals/variable_cleanup

Demonstrates the cleaning of signed 8-bit integers (int8) in Solidity. It shows how invalid values, whether negative or positive, are cleaned by sign extension, where higher bits are set to the sign bit (1 for negative, 0 for positive).

```solidity
1111...1111 1111 1111
1111...1111 1111 1110
....
1111...1111 1000 0000

0000...0000 0000 0000
0000...0000 0000 0001
0000...0000 0000 0010
....
0000...0000 1111 1111

0010...1010 1111 1111   invalid value
1111...1111 1111 1111   cleaned value

1101...0101 0000 0100   invalid value
0000...0000 0000 0100   cleaned value
```

--------------------------------

### Extract Solidity Test Cases for Fuzzing

Source: https://docs.soliditylang.org/en/v0.8.30/contributing

Commands to create a directory for test cases and extract them using the 'isolate_tests.py' script from Solidity's test suite or documentation.

```bash
mkdir /tmp/test_cases
cd /tmp/test_cases
# extract from tests:
path/to/solidity/scripts/isolate_tests.py path/to/solidity/test/libsolidity/SolidityEndToEndTest.cpp
# extract from documentation:
path/to/solidity/scripts/isolate_tests.py path/to/solidity/docs
```

--------------------------------

### Activating Yul Optimizer with Solc

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Shows how to enable the Yul optimizer during the compilation process using the Solidity compiler (solc). It includes flags for strict assembly mode and specifying the number of optimization runs.

```bash
solc --strict-assembly --optimize --optimize-runs 200
```

--------------------------------

### Link Libraries via solc Standard JSON Interface

Source: https://docs.soliditylang.org/en/v0.8.30/using-the-compiler

Illustrates how to specify library addresses within the 'libraries' key of the standard JSON input for the solc compiler. This method is recommended for automated workflows.

```json
{
  "sources": {
    "file.sol": {
      "content": "contract Test { function foo() public pure { Heap h = new Heap(); } }"
    }
  },
  "settings": {
    "libraries": {
      "file.sol": {
        "Heap": "0xabCD567890123456789012345678901234567890"
      }
    }
  }
}
```

--------------------------------

### Solidity: Initial SSA Conversion (UnusedAssignEliminator)

Source: https://docs.soliditylang.org/en/v0.8.30/internals/optimizer

Illustrates the initial SSA conversion of a simple Solidity snippet, showing unnecessary assignments that the UnusedAssignEliminator will later remove.

```solidity
{
    let a_1 := 1
    let a := a_1
    let a_2 := mload(a_1)
    a := a_2
    let a_3 := sload(a_2)
    a := a_3
    sstore(a_3, 1)
}
```

--------------------------------

### Solidity Balances Getter Function

Source: https://docs.soliditylang.org/en/v0.8.30/introduction-to-smart-contracts

The automatically generated getter function for the 'balances' mapping in the Solidity 'Coin' contract. It allows querying the balance of a specific account.

```solidity
function balances(address account) external view returns (uint) {
    return balances[account];
}

```

--------------------------------

### Solidity Compiler Command-Line: Metadata Hash Options

Source: https://docs.soliditylang.org/en/v0.8.30/060-breaking-changes

Demonstrates the command-line options for controlling the metadata hash appended to bytecode. Options include `ipfs`, `swarm`, and `none`.

```bash
# Append IPFS hash (default in 0.8.30+)
solc --metadata-hash ipfs ...

# Append Swarm hash (default before 0.6.0)
solc --metadata-hash swarm ...

# Remove metadata hash
solc --metadata-hash none ...
```

--------------------------------

### Solidity: Truncation of Large Byte Sizes to Address

Source: https://docs.soliditylang.org/en/v0.8.30/types

Illustrates how large byte sizes, like bytes32, are truncated when converted to an address type. The compiler forces explicit truncation to reduce ambiguity. This example shows two ways to convert a 32-byte value, resulting in different 20-byte addresses due to truncation.

```solidity
pragma solidity ^0.4.24;

contract TruncationExample {
    function truncateBytes32() public pure returns (address, address) {
        bytes32 b = 0x111122223333444455556666777788889999AAAABBBBCCCCDDDDEEEEFFFFCCCC;
        
        // Truncates to the last 20 bytes
        address truncated1 = address(uint160(bytes20(b))); 
        
        // Converts to uint256 first, then truncates
        address truncated2 = address(uint160(uint256(b))); 
        
        return (truncated1, truncated2);
    }
}
```

--------------------------------

### Solidity: Selfdestruct Functionality

Source: https://docs.soliditylang.org/en/v0.8.30/units-and-global-variables

The `selfdestruct` function in Solidity destroys the current contract, sending its funds to a specified address. Its behavior, particularly regarding contract destruction versus fund transfer, is dependent on the EVM version. It is also deprecated starting from Solidity 0.8.18.

```Solidity
selfdestruct(address payable recipient)
```

--------------------------------

### Solidity Experimental SMTChecker Pragma

Source: https://docs.soliditylang.org/en/v0.8.30/layout-of-source-files

Enables the SMTChecker component, which provides additional safety warnings by querying an SMT solver. This feature might not support all Solidity language features and could produce many warnings.

```solidity
pragma experimental SMTChecker;

```

--------------------------------

### Solidity memory allocation with potential free memory pointer overflow

Source: https://docs.soliditylang.org/en/v0.8.30/ir-breaking-changes

Shows an example of allocating a large array in Solidity, which can lead to a free memory pointer overflow in the new code generator, causing a revert. The old code generator might run out of gas.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >0.8.0;
contract C {
    function f() public {
        uint[] memory arr;
        // allocation size: 576460752303423481
        // assumes freeMemPtr points to 0x80 initially
        uint solYulMaxAllocationBeforeMemPtrOverflow = (type(uint64).max - 0x80 - 31) / 32;
        // freeMemPtr overflows UINT64_MAX
        arr = new uint[](solYulMaxAllocationBeforeMemPtrOverflow);
    }
}
```

--------------------------------

### Solidity: Original Snippet Before SSA Transformation

Source: https://docs.soliditylang.org/en/v0.8.30/internals/optimizer

Presents the original, simple Solidity code snippet before any SSA transformations are applied.

```solidity
{
    let a := 1
    a := mload(a)
    a := sload(a)
    sstore(a, 1)
}
```

--------------------------------

### Solidity Source File Definition (Content)

Source: https://docs.soliditylang.org/en/v0.8.30/using-the-compiler

Provides Solidity source code directly as a string literal. This is an alternative to specifying URLs for source files.

```json
{
  "content": "contract settable is owned { uint256 private x = 0; function set(uint256 _x) public { if (msg.sender == owner) x = _x; } }"
}
```

--------------------------------

### Solidity: Intermediate Conversions Between Integers and Bytes

Source: https://docs.soliditylang.org/en/v0.8.30/types

Illustrates how to convert between integers and fixed-size byte arrays of different sizes using intermediate conversions to explicitly define padding and truncation rules.

```solidity
bytes2 a = 0x1234;
uint32 b = uint16(a); // b will be 0x00001234
uint32 c = uint32(bytes4(a)); // c will be 0x12340000
uint8 d = uint8(uint16(a)); // d will be 0x34
uint8 e = uint8(bytes1(a)); // e will be 0x12

```

--------------------------------

### Debug Build Configuration

Source: https://docs.soliditylang.org/en/v0.8.30/contributing

Configures the build process to include debug symbols, enabling debugging of tests with the `--debug` flag in GDB.

```shell
cmake -DCMAKE_BUILD_TYPE=Debug ..
make
```

--------------------------------

### Solidity Error Handling with Revert

Source: https://docs.soliditylang.org/en/v0.8.30/introduction-to-smart-contracts

Demonstrates the use of custom errors with the `revert` statement in Solidity. This allows for more informative error messages when a transaction fails.

```solidity
pragma solidity ^0.8.30;

contract ErrorExample {
    error CustomError(string message);

    function doSomething(bool condition) public {
        if (!condition) {
            revert CustomError("Operation failed due to invalid condition.");
        }
        // Proceed with operation
    }
}
```

--------------------------------

### Custom Yul Optimizer Sequence

Source: https://docs.soliditylang.org/en/v0.8.30/internals/optimizer

Allows overriding the default Yul optimization sequence with a custom one using the --yul-optimizations flag. The order of steps is significant, and repeating steps can be beneficial. Brackets [] denote steps applied repeatedly until no change, and a colon : separates the main sequence from a custom cleanup sequence.

```bash
solc --optimize --ir-optimized --yul-optimizations 'dhfoD[xarrscLMcCTU]uljmul:fDnTOcmu'
```

--------------------------------

### List All Soltest Unit Tests

Source: https://docs.soliditylang.org/en/v0.8.30/contributing

Displays a human-readable list of all unit tests executed by the Soltest application.

```shell
./build/test/soltest --list_content=HRF
```

--------------------------------

### Solidity Model Checker Configuration

Source: https://docs.soliditylang.org/en/v0.8.30/using-the-compiler

Configuration for the Solidity model checker, specifying contracts for analysis, division/modulo handling, engine choice, external call trust, invariant reporting, output options, solvers, checked targets, and query timeout.

```json
{
  "modelChecker": {
    "contracts": {
      "source1.sol": ["contract1"],
      "source2.sol": ["contract2", "contract3"]
    },
    "divModNoSlacks": false,
    "engine": "chc",
    "extCalls": "trusted",
    "invariants": ["contract", "reentrancy"],
    "showProvedSafe": true,
    "showUnproved": true,
    "showUnsupported": true,
    "solvers": ["cvc5", "smtlib2", "z3"],
    "targets": ["underflow", "overflow", "assert"],
    "timeout": 20000
  }
}
```

--------------------------------

### Select Model Checker Solvers (CLI)

Source: https://docs.soliditylang.org/en/v0.8.30/smtchecker

Chooses the SMT and Horn solvers to be utilized by the model checker. Available options are 'all', 'cvc5', 'eld', 'smtlib2', and 'z3'. This CLI option enables users to specify preferred backend solvers.

```bash
--model-checker-solvers {all,cvc5,eld,smtlib2,z3}
```

--------------------------------

### Solidity Base Constructors with Arguments

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Illustrates different ways to handle base contract constructors with arguments in Solidity. It shows direct specification in the inheritance list, using modifier-style invocation in the derived constructor, and handling abstract base contracts.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

contract Base {
    uint x;
    constructor(uint x_) {
        x = x_;
    }
}

// Either directly specify in the inheritance list...
contract Derived1 is Base(7) {
    constructor() {}
}

// or through a "modifier" of the derived constructor...
contract Derived2 is Base {
    constructor(uint y) Base(y * y) {}
}

// or declare abstract...
abstract contract Derived3 is Base {
}

// and have the next concrete derived contract initialize it.
contract DerivedFromDerived is Derived3 {
    constructor() Base(10 + 10) {}
}

```

--------------------------------

### Solidity Contract Creation (create2)

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Creates a new contract using the CREATE2 opcode. It takes the amount of ether to send, the memory offset of the initialization code, the size of the initialization code, and a salt. Returns the address of the newly created contract or 0 on error.

```Solidity
address newContract = address(uint160(uint256(keccak256(0xff, address(this), salt, keccak256(init_code))))));
// Example usage:
// newContract = create2(0, abi.encodePacked(init_code), init_code.length, salt);
```

--------------------------------

### Solidity Dynamic Memory Array Creation

Source: https://docs.soliditylang.org/en/v0.8.30/types

Demonstrates the creation of dynamic memory arrays in Solidity using the `new` keyword. It shows how to create an array of arrays and populate it with data, as well as how to create a dynamic byte array and fill it with values.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

contract ArrayContract {
    function createMemoryArray(uint size) public pure returns (bytes memory) {
        // Dynamic memory arrays are created using `new`:
        uint[2][] memory arrayOfPairs = new uint[2][](size);

        // Inline arrays are always statically-sized and if you only
        // use literals, you have to provide at least one type.
        arrayOfPairs[0] = [uint(1), 2];

        // Create a dynamic byte array:
        bytes memory b = new bytes(200);
        for (uint i = 0; i < b.length)
            b[i] = bytes1(uint8(i));
        return b;
    }
}

```

--------------------------------

### Solidity Documentation: Return Parameter Tagging

Source: https://docs.soliditylang.org/en/v0.8.30/060-breaking-changes

Provides guidance on documenting named return parameters in Solidity using the `@return` tag, ensuring the parameter name precedes the description.

```solidity
/**
 * @dev A function that returns a value.
 * @return value The description of the returned value.
 */
function f() public returns (uint value) {
    value = 1;
    return value;
}
```

--------------------------------

### Solidity Function Call with Named Parameters

Source: https://docs.soliditylang.org/en/v0.8.30/control-structures

Shows how to call a function using named parameters, allowing arguments to be provided in any order. This enhances code readability and maintainability.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

contract C {
    mapping(uint => uint) data;

    function f() public {
        set({value: 2, key: 3});
    }

    function set(uint key, uint value) public {
        data[key] = value;
    }
}
```

--------------------------------

### Solidity Contract Demonstrating Data Locations

Source: https://docs.soliditylang.org/en/v0.8.30/types

This Solidity contract showcases the usage and behavior of 'storage', 'memory', and 'calldata' data locations. It demonstrates assignments, referencing, copying, and function calls with different data locations, highlighting interactions between them.

```solidity

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.5.0 <0.9.0;

contract C {
    // The data location of x is storage.
    // This is the only place where the
    // data location can be omitted.
    uint[] x;

    // The data location of memoryArray is memory.
    function f(uint[] memory memoryArray) public {
        x = memoryArray; // works, copies the whole array to storage
        uint[] storage y = x; // works, assigns a pointer, data location of y is storage
        y[7]; // fine, returns the 8th element
        y.pop(); // fine, modifies x through y
        delete x; // fine, clears the array, also modifies y
        // The following does not work; it would need to create a new temporary /
        // unnamed array in storage, but storage is "statically" allocated:
        // y = memoryArray;
        // Similarly, "delete y" is not valid, as assignments to local variables
        // referencing storage objects can only be made from existing storage objects.
        // It would "reset" the pointer, but there is no sensible location it could point to.
        // For more details see the documentation of the "delete" operator.
        // delete y;
        g(x); // calls g, handing over a reference to x
        h(x); // calls h and creates an independent, temporary copy in memory
    }

    function g(uint[] storage) internal pure {}
    function h(uint[] memory) public pure {}
}

```

--------------------------------

### Run Specific Test Cases

Source: https://docs.soliditylang.org/en/v0.8.30/contributing

Executes a subset or specific test cases using filters. The filter can be a precise test name or a wildcard pattern.

```shell
./scripts/soltest.sh -t TestSuite/TestName
```

```shell
./scripts/soltest.sh -t "yulOptimizerTests/disambiguator/*" --no-smt
```

--------------------------------

### Solidity: Using revert and require for error handling

Source: https://docs.soliditylang.org/en/v0.8.30/control-structures

Demonstrates how to use the `revert` statement and the `revert()` function to halt execution and revert state changes, similar to the `require` function. It shows handling insufficient Ether and unauthorized access.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.4;

contract VendingMachine {
    address owner;
    error Unauthorized();
    function buy(uint amount) public payable {
        if (amount > msg.value / 2 ether)
            revert("Not enough Ether provided.");
        // Alternative way to do it:
        require(
            amount <= msg.value / 2 ether,
            "Not enough Ether provided."
        );
        // Perform the purchase.
    }
    function withdraw() public {
        if (msg.sender != owner)
            revert Unauthorized();

        payable(msg.sender).transfer(address(this).balance);
    }
}
```

--------------------------------

### Simplified Solidity Code After Optimization

Source: https://docs.soliditylang.org/en/v0.8.30/internals/optimizer

This is the simplified version of the previous Solidity code snippet after the optimizer has evaluated the condition and removed the unnecessary branch.

```solidity
data[7] = 9;
return 1;

```

--------------------------------

### Solidity Compiler Command for Documentation

Source: https://docs.soliditylang.org/en/v0.8.30/natspec-format

This command uses the Solidity compiler (`solc`) to generate both user documentation (`--userdoc`) and developer documentation (`--devdoc`) for a given Solidity file. The output is typically in JSON format.

```bash
solc --userdoc --devdoc ex1.sol

```

--------------------------------

### Solidity Contract Documentation with NatSpec Tags

Source: https://docs.soliditylang.org/en/v0.8.30/natspec-format

This snippet demonstrates a Solidity smart contract with comprehensive NatSpec comments. It includes tags for title, author, notice, dev, custom experimental features, parameter descriptions, return values, and inheritance documentation (@inheritdoc). The comments are essential for generating documentation and providing user-facing information during contract interaction.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.2 < 0.9.0;

/// @title A simulator for trees
/// @author Larry A. Gardner
/// @notice You can use this contract for only the most basic simulation
/// @dev All function calls are currently implemented without side effects
/// @custom:experimental This is an experimental contract.
contract Tree {
    /// @notice Calculate tree age in years, rounded up, for live trees
    /// @dev The Alexandr N. Tetearing algorithm could increase precision
    /// @param rings The number of rings from dendrochronological sample
    /// @return Age in years, rounded up for partial years
    /// @return Name of the tree
    function age(uint256 rings) external virtual pure returns (uint256, string memory) {
        return (rings + 1, "tree");
    }

    /// @notice Returns the amount of leaves the tree has.
    /// @dev Returns only a fixed number.
    function leaves() external virtual pure returns(uint256) {
        return 2;
    }
}

contract Plant {
    function leaves() external virtual pure returns(uint256) {
        return 3;
    }
}

contract KumquatTree is Tree, Plant {
    function age(uint256 rings) external override pure returns (uint256, string memory) {
        return (rings + 2, "Kumquat");
    }

    /// Return the amount of leaves that this specific kind of tree has
    /// @inheritdoc Tree
    function leaves() external override(Tree, Plant) pure returns(uint256) {
        return 3;
    }
}

```

--------------------------------

### Solidity Abstract Contract Inheritance

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Demonstrates a concrete contract 'Cat' inheriting from the abstract contract 'Feline' and implementing the 'utterance' function. This shows how to provide implementations for abstract functions.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

abstract contract Feline {
    function utterance() public pure virtual returns (bytes32);
}

contract Cat is Feline {
    function utterance() public pure override returns (bytes32) { return "miaow"; }
}
```

--------------------------------

### Solidity Contract Definition

Source: https://docs.soliditylang.org/en/v0.8.30/abi-spec

Defines a sample Solidity contract 'Foo' with three functions: 'bar', 'baz', and 'sam'. 'bar' takes a fixed-size byte array, 'baz' takes a uint32 and a bool, and 'sam' takes a dynamic byte array, a bool, and a dynamic array of uints.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract Foo {
    function bar(bytes3[2] memory) public pure {}
    function baz(uint32 x, bool y) public pure returns (bool r) { r = x > 32 || y; }
    function sam(bytes memory, bool, uint[] memory) public pure {}
}

```

--------------------------------

### Build Solidity with AFL for Fuzzing

Source: https://docs.soliditylang.org/en/v0.8.30/contributing

This sequence builds the Solidity compiler, specifically the 'solfuzzer' binary, using AFL (American Fuzzy Lop) as the C/C++ compiler. This instrumentation helps in finding internal compiler errors.

```bash
cd build
# if needed
make clean
cmake .. -DCMAKE_C_COMPILER=path/to/afl-gcc -DCMAKE_CXX_COMPILER=path/to/afl-g++
make solfuzzer

```

--------------------------------

### Set EVM Version via solc Standard JSON Interface

Source: https://docs.soliditylang.org/en/v0.8.30/using-the-compiler

Demonstrates how to configure the target EVM version within the 'settings' object of the standard JSON input for the solc compiler. This is the recommended approach for programmatic compilation.

```json
{
  "sources": {/* ... */},
  "settings": {
    "optimizer": {/* ... */},
    "evmVersion": "<VERSION>"
  }
}
```

--------------------------------

### Solidity Debugging Settings

Source: https://docs.soliditylang.org/en/v0.8.30/using-the-compiler

Configures how revert strings and debugging information are handled during compilation. `revertStrings` controls the inclusion of reason strings, while debug information can include source location annotations.

```json
{
    "debug": {
      "revertStrings": "default"
    }
  }
```

--------------------------------

### Solidity Conditional Logic Simplification

Source: https://docs.soliditylang.org/en/v0.8.30/internals/optimizer

This Solidity code demonstrates a conditional statement where the condition is always false, showing how the optimizer can simplify the control flow.

```solidity
uint x = 7;
data[7] = 9;
if (data[x] != x + 2) // this condition is never true
  return 2;
else
  return 1;

```

--------------------------------

### EVM Dialect Return Data and Contract Creation

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Opcodes related to handling return data from previous calls and creating new contracts. 'returndatasize' and 'returndatacopy' manage data returned by a call, while 'create' is used to deploy new contracts.

```solidity
returndatasize()
returndatacopy(t, f, s)
create(v, p, n)
```

--------------------------------

### Solidity Salted Contract Creation with 'create2'

Source: https://docs.soliditylang.org/en/v0.8.30/control-structures

Explains and demonstrates salted contract creations using 'create2' in Solidity. This method computes the new contract's address using a salt, the creating contract's address, the creation bytecode, and constructor arguments, rather than a counter. This allows for predictable address derivation.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;
contract D {
    uint public x;
    constructor(uint a) {
        x = a;
    }
}

contract C {
    function createDSalted(bytes32 salt, uint arg) public {
        // This complicated expression just tells you how the address
        // can be pre-computed. It is just there for illustration.
        // You actually only need ``new D{salt: salt}(arg)``.
        address predictedAddress = address(uint160(uint(keccak256(abi.encodePacked(
            bytes1(0xff),
            address(this),
            salt,
            keccak256(abi.encodePacked(
                type(D).creationCode, 
                abi.encode(arg)
            ))
        )))));

        D d = new D{salt: salt}(arg);
        require(address(d) == predictedAddress);
    }
}
```

--------------------------------

### Run Boost C++ Test Framework Tests

Source: https://docs.soliditylang.org/en/v0.8.30/contributing

Executes tests bundled within the Boost C++ Test Framework application. This is sufficient for most code changes.

```shell
build/test/soltest
```

```shell
scripts/soltest.sh
```

--------------------------------

### Yul - Basic Operations and Variable Assignment

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Demonstrates a simple Yul operation involving string literal 'abc', addition, bitwise AND, and assignment to a variable 'x'. It showcases basic arithmetic and bitwise operations within Yul.

```Yul
let x := and("abc", add(3, 2))
```

--------------------------------

### Solidity Proxy Contract for Forwarding Calls

Source: https://docs.soliditylang.org/en/v0.8.30/types

This Solidity contract demonstrates how to forward calls to another contract using `delegatecall`. It includes basic validation for the `setOwner` function signature and argument, showcasing the use of array slicing for ABI decoding.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.5 <0.9.0;
contract Proxy {
    /// @dev Address of the client contract managed by proxy i.e., this contract
    address client;

    constructor(address client_) {
        client = client_;
    }

    /// Forward call to "setOwner(address)" that is implemented by client
    /// after doing basic validation on the address argument.
    function forward(bytes calldata payload) external {
        bytes4 sig = bytes4(payload[:4]);
        // Due to truncating behavior, bytes4(payload) performs identically.
        // bytes4 sig = bytes4(payload);
        if (sig == bytes4(keccak256("setOwner(address)"))) {
            address owner = abi.decode(payload[4:], (address));
            require(owner != address(0), "Address of owner cannot be zero.");
        }
        (bool status,) = client.delegatecall(payload);
        require(status, "Forwarded call failed.");
    }
}

```

--------------------------------

### Bytecode Source Mapping Notation and Encoding

Source: https://docs.soliditylang.org/en/v0.8.30/internals/source_mappings

Details the more complex encoding for source mappings associated with bytecode. It includes jump type and modifier depth information, with compression rules for efficiency.

```text
`s:l:f:j:m` separated by `;`
Each element corresponds to an instruction. `s`, `l`, `f` are as above. `j` signifies jump type ('i', 'o', or '-'). `m` denotes modifier depth.
```

--------------------------------

### Solidity Mint Function with Access Control

Source: https://docs.soliditylang.org/en/v0.8.30/introduction-to-smart-contracts

Illustrates a `mint` function in Solidity that allows only the contract creator (`minter`) to mint new tokens. It uses `require` to enforce this condition and includes checked arithmetic to prevent overflows.

```solidity
pragma solidity ^0.8.30;

contract Token {
    mapping(address => uint) public balances;
    address public minter;

    constructor() {
        minter = msg.sender;
    }

    function mint(address receiver, uint amount) public {
        require(msg.sender == minter, "Only the minter can mint tokens.");
        balances[receiver] += amount; // Potential overflow handled by default checked arithmetic
    }
}
```

--------------------------------

### Yul Stand-Alone Usage with Solidity Compiler (JSON)

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Configuration for using Yul in stand-alone mode with the Solidity compiler via JSON interface. It specifies the language as Yul, provides a simple Yul code snippet for storage, and enables optimizer details for Yul.

```JSON
{
    "language": "Yul",
    "sources": { "input.yul": { "content": "{ sstore(0, 1) }" } },
    "settings": {
        "outputSelection": { "*": { "*": ["*"] } },
        "optimizer": { "enabled": true, "details": { "yul": true } }
    }
}
```

--------------------------------

### Solidity Function Type Declaration Syntax

Source: https://docs.soliditylang.org/en/v0.8.30/types

Illustrates the syntax for declaring function types in Solidity. It covers the structure for specifying parameters, visibility (internal/external), state mutability (pure/view/payable), and return types.

```solidity
function (<parameter types>) {internal|external} [pure|view|payable] [returns (<return types>)]

```

--------------------------------

### Solidity ABI Coder Pragma

Source: https://docs.soliditylang.org/en/v0.8.30/layout-of-source-files

Specifies which ABI encoder/decoder implementation to use. `v2` supports nested arrays and structs, offering more validation at potentially higher gas costs. It's the default from 0.8.0 onwards. `v1` can be explicitly selected.

```solidity
pragma abicoder v1;

```

```solidity
pragma abicoder v2;

```

--------------------------------

### Specify Solidity Compiler Version Pragma

Source: https://docs.soliditylang.org/en/v0.8.30/layout-of-source-files

This code illustrates how to use the `pragma` keyword to specify the compatible Solidity compiler version. It ensures the contract is compiled with a suitable compiler version, preventing potential issues with future breaking changes.

```Solidity
pragma solidity ^0.5.2;
```

--------------------------------

### Remapping affecting VFS Source Unit Name

Source: https://docs.soliditylang.org/en/v0.8.30/path-resolution

Shows a remapping that affects how the compiler names a source unit in the Virtual File System (VFS). Here, '/project/' is remapped to '/contracts/', resulting in the source unit name '/contracts/contract.sol' for '/project/contract.sol'.

```bash
solc /project/=/contracts/ /project/contract.sol # source unit name: /contracts/contract.sol
```

--------------------------------

### Watching for Contract Events with web3.js

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

This JavaScript code snippet shows how to interact with a deployed Solidity contract using web3.js to watch for a specific event ('Deposit'). It includes methods for both watching changes and passing an immediate callback.

```javascript
var abi = /* abi as generated by the compiler */;
var ClientReceipt = web3.eth.contract(abi);
var clientReceipt = ClientReceipt.at("0x1234...ab67" /* address */);

var depositEvent = clientReceipt.Deposit();

// watch for changes
depositEvent.watch(function(error, result){
    // result contains non-indexed arguments and topics
    // given to the `Deposit` call.
    if (!error)
        console.log(result);
});


// Or pass a callback to start watching immediately
var depositEvent = clientReceipt.Deposit(function(error, result) {
    if (!error)
        console.log(result);
});

```

--------------------------------

### Yul - Function Call and Stack Operations

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Shows how to call a user-defined function 'f' that returns two values, assigning them to local variables 'x' and 'y'. It also demonstrates modifying memory using built-in functions like mstore and mload.

```Yul
function f(x, y) -> a, b { /* ... */ }
mstore(0x80, add(mload(0x80), 3))
// Here, the user-defined function `f` returns two values.
let x, y := f(1, mload(0))
```

--------------------------------

### Select Model Checker Engine (CLI)

Source: https://docs.soliditylang.org/en/v0.8.30/smtchecker

Specifies the model checking engine to be used. Options include 'all' (default), 'bmc', 'chc', and 'none'. This command-line interface option allows direct control over the verification process.

```bash
--model-checker-engine {all,bmc,chc,none}
```

--------------------------------

### For Loop Initialization Transformation

Source: https://docs.soliditylang.org/en/v0.8.30/internals/optimizer

Moves the initialization part of a for loop to before the loop itself. This simplifies optimization by eliminating complex for loop initialization scoping rules. The transformation changes `for { Init } C { Post } { Body }` to `Init ... for {} C { Post } { Body }`.

```solidity
for { Init... } C { Post... } {
    Body...
}

is transformed to

Init...
for {} C { Post... } {
    Body...
}
```

--------------------------------

### Solidity A Storage Layout

Source: https://docs.soliditylang.org/en/v0.8.30/internals/layout_in_storage

Illustrates the storage layout for a Solidity contract 'A', showing how data is arranged in storage slots.

```Solidity
00 [iiiiiiiiiiiiiiiibbbbbbbbbbbbbbbb]
00 [aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa]
```

--------------------------------

### Solidity Constructor and State Variables

Source: https://docs.soliditylang.org/en/v0.8.30/introduction-to-smart-contracts

Demonstrates a Solidity constructor that stores the contract creator's address. It highlights the use of `msg.sender` to access the caller's address and permanently store it within the contract.

```solidity
pragma solidity ^0.8.30;

contract MyContract {
    address public owner;

    constructor() {
        owner = msg.sender;
    }
}
```

--------------------------------

### Solidity Utility Functions

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Provides helper functions for common operations like comparison (lte, gte), safe addition with overflow checking, caller verification, and address validation. Includes a generic require function.

```Solidity
/* ---------- utility functions ---------- */
            function lte(a, b) -> r {
                r := iszero(gt(a, b))
            }
            function gte(a, b) -> r {
                r := iszero(lt(a, b))
            }
            function safeAdd(a, b) -> r {
                r := add(a, b)
                if or(lt(r, a), lt(r, b)) { revert(0, 0) }
            }
            function calledByOwner() -> cbo {
                cbo := eq(owner(), caller())
            }
            function revertIfZeroAddress(addr) {
                require(addr)
            }
            function require(condition) {
                if iszero(condition) { revert(0, 0) }
            }
```

--------------------------------

### Solidity Interface Inheritance

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Demonstrates interface inheritance in Solidity, where 'SubInterface' inherits from 'ParentA' and 'ParentB'. It shows how to redefine functions to assert compatibility between parent interfaces.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.2 <0.9.0;

interface ParentA {
    function test() external returns (uint256);
}

interface ParentB {
    function test() external returns (uint256);
}

interface SubInterface is ParentA, ParentB {
    // Must redefine test in order to assert that the parent
    // meanings are compatible.
    function test() external override(ParentA, ParentB) returns (uint256);
}
```

--------------------------------

### Initialize Dynamically-Sized Memory Arrays in Solidity

Source: https://docs.soliditylang.org/en/v0.8.30/types

Illustrates the correct way to initialize dynamically-sized memory arrays by first allocating the array with 'new' and then assigning individual elements, as direct assignment from literals is not supported.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract C {
    function f() public pure {
        uint[] memory x = new uint[](3);
        x[0] = 1;
        x[1] = 3;
        x[2] = 4;
    }
}

```

--------------------------------

### Solidity Import without base path consideration

Source: https://docs.soliditylang.org/en/v0.8.30/path-resolution

Shows a Solidity import statement that does not rely on the base path for resolution due to specific remapping rules. The import 'util.sol' is resolved directly to 'util.sol' because the base path modification is bypassed by the remapping configuration.

```solidity
import "util.sol" as util; // source unit name: util.sol
```

--------------------------------

### Solidity Ether Unit Conversions

Source: https://docs.soliditylang.org/en/v0.8.30/units-and-global-variables

Demonstrates the conversion of Ether units (wei, gwei, ether) in Solidity. Asserts the equivalency of different denominations, with wei being the base unit.

```solidity
assert(1 wei == 1);
assert(1 gwei == 1e9);
assert(1 ether == 1e18);
```

--------------------------------

### Solidity Deployed Bytecode Structure

Source: https://docs.soliditylang.org/en/v0.8.30/using-the-compiler

Details the structure of deployed Solidity bytecode, including immutable references and their locations within the bytecode. This is crucial for understanding how contract state is stored and accessed.

```json
{
  "deployedBytecode": {
    "immutableReferences": {
      "3": [
        { "start": 42, "length": 32 },
        { "start": 80, "length": 32 }
      ]
    }
  },
  "methodIdentifiers": {
    "delegate(address)": "5c19a95c"
  },
  "gasEstimates": {
    "creation": {
      "codeDepositCost": "420000",
      "executionCost": "infinite",
      "totalCost": "infinite"
    },
    "external": {
      "delegate(address)": "25000"
    },
    "internal": {
      "heavyLifting()": "infinite"
    }
  }
}
```

--------------------------------

### Solidity ERC20-like Token Functions

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Implements core functionalities for a token contract, including total supply, balance tracking, minting, and allowance management. Uses SLOAD and SSTORE for state manipulation.

```Solidity
o := sload(ownerPos())
            }
            function totalSupply() -> supply {
                supply := sload(totalSupplyPos())
            }
            function mintTokens(amount) {
                sstore(totalSupplyPos(), safeAdd(totalSupply(), amount))
            }
            function balanceOf(account) -> bal {
                bal := sload(accountToStorageOffset(account))
            }
            function addToBalance(account, amount) {
                let offset := accountToStorageOffset(account)
                sstore(offset, safeAdd(sload(offset), amount))
            }
            function deductFromBalance(account, amount) {
                let offset := accountToStorageOffset(account)
                let bal := sload(offset)
                require(lte(amount, bal))
                sstore(offset, sub(bal, amount))
            }
            function allowance(account, spender) -> amount {
                amount := sload(allowanceStorageOffset(account, spender))
            }
            function setAllowance(account, spender, amount) {
                sstore(allowanceStorageOffset(account, spender), amount)
            }
            function decreaseAllowanceBy(account, spender, amount) {
                let offset := allowanceStorageOffset(account, spender)
                let currentAllowance := sload(offset)
                require(lte(amount, currentAllowance))
                sstore(offset, sub(currentAllowance, amount))
            }
```

--------------------------------

### Solidity: Check balance and transfer Ether

Source: https://docs.soliditylang.org/en/v0.8.30/types

Demonstrates querying an address's balance and sending Ether using 'balance' and 'transfer'. The 'transfer' function reverts on failure, and executing it on a contract address can trigger the recipient's receive or fallback function.

```Solidity
address payable x = payable(0x123);
address myAddress = address(this);
if (x.balance < 10 && myAddress.balance >= 10) x.transfer(10);
```

--------------------------------

### Solidity User Documentation JSON Output

Source: https://docs.soliditylang.org/en/v0.8.30/natspec-format

This JSON structure represents the user-facing documentation generated by the Solidity compiler. It includes versioning information, the documentation kind ('user'), and method-specific notices.

```json
{
  "version" : 1,
  "kind" : "user",
  "methods" :
  {
    "age(uint256)" :
    {
      "notice" : "Calculate tree age in years, rounded up, for live trees"
    },
    "leaves()" :
    {
        "notice" : "Returns the amount of leaves the tree has."
    }
  },
  "notice" : "You can use this contract for only the most basic simulation"
}

```

--------------------------------

### Compiler Output Structure

Source: https://docs.soliditylang.org/en/v0.8.30/using-the-compiler

This section describes the overall JSON structure of the Solidity compiler's output, including potential errors, source file details, and contract-specific information.

```APIDOC
## Compiler Output Structure

### Description
This document outlines the JSON structure returned by the Solidity compiler. It details the organization of error messages, source file analysis, and contract-specific outputs like ABI, bytecode, and metadata.

### Endpoint
N/A (Compiler Output)

### Response
#### Success Response (200)
- **errors** (array) - Optional: Contains a list of errors, warnings, or informational messages encountered during compilation. Each error object includes severity, type, message, and optional source location details.
- **sources** (object) - Contains details about the processed source files, including their ASTs.
- **contracts** (object) - Contains contract-level outputs, including ABI, metadata, user/developer documentation, EVM-related information (bytecode, assembly, source maps), and storage layout.

#### Response Example
```json
{
  "errors": [
    {
      "sourceLocation": {
        "file": "sourceFile.sol",
        "start": 0,
        "end": 100
      },
      "secondarySourceLocations": [
        {
          "file": "sourceFile.sol",
          "start": 64,
          "end": 92,
          "message": "Other declaration is here:"
        }
      ],
      "type": "TypeError",
      "component": "general",
      "severity": "error",
      "errorCode": "3141",
      "message": "Invalid keyword",
      "formattedMessage": "sourceFile.sol:100: Invalid keyword"
    }
  ],
  "sources": {
    "sourceFile.sol": {
      "id": 1,
      "ast": {}
    }
  },
  "contracts": {
    "sourceFile.sol": {
      "ContractName": {
        "abi": [],
        "metadata": "{/* ... */}",
        "userdoc": {},
        "devdoc": {},
        "ir": "",
        "irAst":  {/* ... */},
        "irOptimized": "",
        "irOptimizedAst": {/* ... */},
        "storageLayout": {"storage": [/* ... */], "types": {/* ... */} },
        "transientStorageLayout": {"storage": [/* ... */], "types": {/* ... */} },
        "evm": {
          "assembly": "",
          "legacyAssembly": {},
          "bytecode": {
            "functionDebugData": {
              "@mint_13": {
                "entryPoint": 128,
                "id": 13,
                "parameterSlots": 2,
                "returnSlots": 1
              }
            },
            "object": "00fe",
            "opcodes": "",
            "sourceMap": "",
            "generatedSources": [
              {
                "ast": {/* ... */},
                "contents":"{ function abi_decode(start, end) -> data { data := calldataload(start) } }",
                "id": 2,
                "language": "Yul",
                "name": "#utility.yul"
              }
            ],
            "linkReferences": {
              "libraryFile.sol": {
                "Library1": [
                  // Byte offsets into the bytecode.
                  // Linking replaces the 20 bytes located there.
                ]
              }
            }
          }
        }
      }
    }
  }
}
```
```

--------------------------------

### Specify Solidity License Identifier

Source: https://docs.soliditylang.org/en/v0.8.30/layout-of-source-files

This snippet demonstrates the required SPDX License Identifier comment at the beginning of a Solidity source file. It helps establish trust by indicating the source code's licensing.

```Solidity
// SPDX-License-Identifier: MIT
```

--------------------------------

### Complete ERC20 Token Implementation in Solidity

Source: https://docs.soliditylang.org/en/v0.8.30/yul

This code snippet provides a comprehensive implementation of the ERC20 token standard in Solidity. It includes functions for minting, transferring, approving, checking balances, and handling allowances. The contract also emits standard ERC20 events for transfers and approvals. It relies on internal helper functions for data decoding, storage manipulation, and event logging.

```Solidity
object "Token" {
    code {
        // Store the creator in slot zero.
        sstore(0, caller())

        // Deploy the contract
        datacopy(0, dataoffset("runtime"), datasize("runtime"))
        return(0, datasize("runtime"))
    }
    object "runtime" {
        code {
            // Protection against sending Ether
            require(iszero(callvalue()))

            // Dispatcher
            switch selector()
            case 0x70a08231 /* "balanceOf(address)" */ {
                returnUint(balanceOf(decodeAsAddress(0)))
            }
            case 0x18160ddd /* "totalSupply()" */ {
                returnUint(totalSupply())
            }
            case 0xa9059cbb /* "transfer(address,uint256)" */ {
                transfer(decodeAsAddress(0), decodeAsUint(1))
                returnTrue()
            }
            case 0x23b872dd /* "transferFrom(address,address,uint256)" */ {
                transferFrom(decodeAsAddress(0), decodeAsAddress(1), decodeAsUint(2))
                returnTrue()
            }
            case 0x095ea7b3 /* "approve(address,uint256)" */ {
                approve(decodeAsAddress(0), decodeAsUint(1))
                returnTrue()
            }
            case 0xdd62ed3e /* "allowance(address,address)" */ {
                returnUint(allowance(decodeAsAddress(0), decodeAsAddress(1)))
            }
            case 0x40c10f19 /* "mint(address,uint256)" */ {
                mint(decodeAsAddress(0), decodeAsUint(1))
                returnTrue()
            }
            default {
                revert(0, 0)
            }

            function mint(account, amount) {
                require(calledByOwner())

                mintTokens(amount)
                addToBalance(account, amount)
                emitTransfer(0, account, amount)
            }
            function transfer(to, amount) {
                executeTransfer(caller(), to, amount)
            }
            function approve(spender, amount) {
                revertIfZeroAddress(spender)
                setAllowance(caller(), spender, amount)
                emitApproval(caller(), spender, amount)
            }
            function transferFrom(from, to, amount) {
                decreaseAllowanceBy(from, caller(), amount)
                executeTransfer(from, to, amount)
            }

            function executeTransfer(from, to, amount) {
                revertIfZeroAddress(to)
                deductFromBalance(from, amount)
                addToBalance(to, amount)
                emitTransfer(from, to, amount)
            }


            /* ---------- calldata decoding functions ----------- */
            function selector() -> s {
                s := div(calldataload(0), 0x100000000000000000000000000000000000000000000000000000000)
            }

            function decodeAsAddress(offset) -> v {
                v := decodeAsUint(offset)
                if iszero(iszero(and(v, not(0xffffffffffffffffffffffffffffffffffffffff)))) {
                    revert(0, 0)
                }
            }
            function decodeAsUint(offset) -> v {
                let pos := add(4, mul(offset, 0x20))
                if lt(calldatasize(), add(pos, 0x20)) {
                    revert(0, 0)
                }
                v := calldataload(pos)
            }
            /* ---------- calldata encoding functions ---------- */
            function returnUint(v) {
                mstore(0, v)
                return(0, 0x20)
            }
            function returnTrue() {
                returnUint(1)
            }

            /* -------- events ---------- */
            function emitTransfer(from, to, amount) {
                let signatureHash := 0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef
                emitEvent(signatureHash, from, to, amount)
            }
            function emitApproval(from, spender, amount) {
                let signatureHash := 0x8c5be1e5ebec7d5bd14f71427d1e84f3dd0314c0f7b2291e5b200ac8c7c3b925
                emitEvent(signatureHash, from, spender, amount)
            }
            function emitEvent(signatureHash, indexed1, indexed2, nonIndexed) {
                mstore(0, nonIndexed)
                log3(0, 0x20, signatureHash, indexed1, indexed2)
            }

            /* -------- storage layout ---------- */
            function ownerPos() -> p { p := 0 }
            function totalSupplyPos() -> p { p := 1 }
            function accountToStorageOffset(account) -> offset {
                offset := add(0x1000, account)
            }
            function allowanceStorageOffset(account, spender) -> offset {
                offset := accountToStorageOffset(account)
                mstore(0, offset)
                mstore(0x20, spender)
                offset := keccak256(0, 0x40)
            }

            /* -------- storage access ---------- */
            function owner() -> o {

```

--------------------------------

### Solidity Crowdfunding Contract with Structs

Source: https://docs.soliditylang.org/en/v0.8.30/types

Demonstrates defining and using structs in Solidity for a crowdfunding scenario. Includes struct definitions for 'Funder' and 'Campaign', and functions for creating campaigns, receiving contributions, and checking funding goals. Structs are used within mappings to manage campaign data.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

// Defines a new type with two fields.
// Declaring a struct outside of a contract allows
// it to be shared by multiple contracts.
// Here, this is not really needed.
struct Funder {
    address addr;
    uint amount;
}

contract CrowdFunding {
    // Structs can also be defined inside contracts, which makes them
    // visible only there and in derived contracts.
    struct Campaign {
        address payable beneficiary;
        uint fundingGoal;
        uint numFunders;
        uint amount;
        mapping(uint => Funder) funders;
    }

    uint numCampaigns;
    mapping(uint => Campaign) campaigns;

    function newCampaign(address payable beneficiary, uint goal) public returns (uint campaignID) {
        campaignID = numCampaigns++; // campaignID is return variable
        // We cannot use "campaigns[campaignID] = Campaign(beneficiary, goal, 0, 0)"
        // because the right hand side creates a memory-struct "Campaign" that contains a mapping.
        Campaign storage c = campaigns[campaignID];
        c.beneficiary = beneficiary;
        c.fundingGoal = goal;
    }

    function contribute(uint campaignID) public payable {
        Campaign storage c = campaigns[campaignID];
        // Creates a new temporary memory struct, initialised with the given values
        // and copies it over to storage.
        // Note that you can also use Funder(msg.sender, msg.value) to initialise.
        c.funders[c.numFunders++] = Funder({addr: msg.sender, amount: msg.value});
        c.amount += msg.value;
    }

    function checkGoalReached(uint campaignID) public returns (bool reached) {
        Campaign storage c = campaigns[campaignID];
        if (c.amount < c.fundingGoal)
            return false;
        uint amount = c.amount;
        c.amount = 0;
        c.beneficiary.transfer(amount);
        return true;
    }
}

```

--------------------------------

### Solidity ABI Encoding and Decoding Functions

Source: https://docs.soliditylang.org/en/v0.8.30/cheatsheet

Provides functions for encoding and decoding data according to the Ethereum ABI specification. Includes functions for general encoding, packed encoding, encoding with a selector, and encoding calls to specific functions.

```Solidity
abi.decode(bytes memory encodedData, (...)) returns (...)
```

```Solidity
abi.encode(...) returns (bytes memory)
```

```Solidity
abi.encodePacked(...) returns (bytes memory)
```

```Solidity
abi.encodeWithSelector(bytes4 selector, ...) returns (bytes memory)
```

```Solidity
abi.encodeCall(function functionPointer, (...)) returns (bytes memory)
```

```Solidity
abi.encodeWithSignature(string memory signature, ...) returns (bytes memory)
```

--------------------------------

### Accessing Integer Limits in Solidity

Source: https://docs.soliditylang.org/en/v0.8.30/types

Shows how to access the minimum and maximum values for a given integer type in Solidity using the `type(X).min` and `type(X).max` syntax, where `X` is the integer type.

```Solidity
// Get the minimum value of uint8
type(uint8).min;

// Get the maximum value of int256
type(int256).max;
```

--------------------------------

### Solidity Compiler Input Structure

Source: https://docs.soliditylang.org/en/v0.8.30/using-the-compiler

Defines the primary JSON structure for interacting with the Solidity compiler. It includes fields for the source code language, source file definitions, and compiler settings.

```json
{
  "language": "Solidity",
  "sources": {
    // Source file definitions go here
  },
  "settings": {
    // Compiler settings go here
  }
}
```

--------------------------------

### Solidity Exponentiation Notes

Source: https://docs.soliditylang.org/en/v0.8.30/types

Provides notes on exponentiation in Solidity, emphasizing its availability only for unsigned exponents and the potential for gas costs or assertion failures. It also mentions the EVM's definition of `0**0` as `1`.

```solidity
// For x**3, the expression x*x*x might be cheaper.
// Note that `0**0` is defined by the EVM as `1`.
```

--------------------------------

### Solidity Fixed Point Operators

Source: https://docs.soliditylang.org/en/v0.8.30/types

Lists the available operators for fixed-point numbers in Solidity, including comparison and arithmetic operators.

```solidity
Operators:
  * Comparisons: `<=`, `<`, `==`, `!=`, `>=`, `>` (evaluate to `bool`)
  * Arithmetic operators: `+`, `-`, unary `-`, `*`, `/`, `%` (modulo)
```

--------------------------------

### Solidity Try/Catch for External Call Error Handling

Source: https://docs.soliditylang.org/en/v0.8.30/control-structures

Demonstrates catching specific errors (Error, Panic, lowLevelData) and generic errors from external calls using try/catch. It shows how to manage error counts and return success status.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.1;

interface DataFeed { function getData(address token) external returns (uint value); }

contract FeedConsumer {
    DataFeed feed;
    uint errorCount;
    function rate(address token) public returns (uint value, bool success) {
        // Permanently disable the mechanism if there are
        // more than 10 errors.
        require(errorCount < 10);
        try feed.getData(token) returns (uint v) {
            return (v, true);
        } catch Error(string memory /*reason*/) {
            // This is executed in case
            // revert was called inside getData
            // and a reason string was provided.
            errorCount++;
            return (0, false);
        } catch Panic(uint /*errorCode*/) {
            // This is executed in case of a panic, i.e. a serious error like division by zero
            // or overflow. The error code can be used to determine the kind of error.
            errorCount++;
            return (0, false);
        } catch (bytes memory /*lowLevelData*/) {
            // This is executed in case revert() was used.
            errorCount++;
            return (0, false);
        }
    }
}
```

--------------------------------

### Create and Use Array Literals in Solidity

Source: https://docs.soliditylang.org/en/v0.8.30/types

Shows how to create array literals with homogeneous types and explicit type conversion for mixed types. Illustrates the base type determination and usage in function calls.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract C {
    function f() public pure {
        g([uint(1), 2, 3]);
    }
    function g(uint[3] memory) public pure {
        // ...
    }
}

```

--------------------------------

### Removal of `--clone-bin` and `--combined-json clone-bin` (Solidity Compiler)

Source: https://docs.soliditylang.org/en/v0.8.30/050-breaking-changes

The Solidity compiler has removed the `--clone-bin` and `--combined-json clone-bin` command-line options. These options were related to specific binary output formats that are no longer supported.

```Shell
# These commands are no longer valid in Solidity 0.8.30+
# solc --clone-bin ...
# solc --combined-json clone-bin ...

# Use alternative methods if similar functionality is needed.
```

--------------------------------

### Select Model Checker Solvers (JSON)

Source: https://docs.soliditylang.org/en/v0.8.30/smtchecker

Configures the model checker's solvers using a JSON settings array. The 'settings.modelChecker.solvers' parameter accepts an array of solver identifiers such as 'smtlib2' and 'z3'.

```json
settings.modelChecker.solvers=[smtlib2,z3]
```

--------------------------------

### Solidity Yul: Variable Assignment and Multiple Return Values

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Shows how to assign values to variables using the ':=' operator, re-assign existing variables, and perform multiple assignments from a function call that returns multiple values in Yul.

```Solidity Yul
let v := 0
// re-assign v
v := 2
let t := add(v, 2)
function f() -> a, b { }
// assign multiple values
v, t := f()

```

--------------------------------

### EVM Assembly Import

Source: https://docs.soliditylang.org/en/v0.8.30/using-the-compiler

Outlines the format for importing EVM Assembly code. This experimental feature requires the `language` to be set to `EVMAssembly` and provides the assembly code in a JSON object.

```json
{
  "assemblyJson": {
    ".code": [ ... ],
    ".data": { ... },
    "sourceList": [ ... ]
  }
}
```

--------------------------------

### Solidity Contract C Storage Layout Visualization

Source: https://docs.soliditylang.org/en/v0.8.30/internals/layout_in_storage

Visual representation of the storage slots for contract 'C', illustrating how variables are packed and where they reside in memory.

```Text
42 [aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa]
43 [eeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee]
44 [ffffffffffffffffffffffffffffffff]
45 [                            hhgg]
46 [                           yxxxx]
47 [          lllllllllllllllllllllk]
48 [                      mmmmmmmmmm]
49 [  nnnnnnnnnnnnnnnnnnnnnnnnnnnnnn]
50 [                      nnnnnnnnnn]
51 [                           ooooo]

```

--------------------------------

### Solidity Low-Level DELEGATECALL

Source: https://docs.soliditylang.org/en/v0.8.30/units-and-global-variables

Performs a low-level DELEGATECALL to an address with a given payload. It forwards all available gas and returns success status and return data. Essential for library-like behavior, but requires aligned storage layouts.

```Solidity
 (bool success, bytes memory returnData) = someAddress.delegatecall(payload); 
```

--------------------------------

### Solidity Developer Documentation JSON Output

Source: https://docs.soliditylang.org/en/v0.8.30/natspec-format

This JSON structure represents the developer-facing documentation generated by the Solidity compiler. It includes versioning, kind ('dev'), author, general details, custom tags, and detailed information about methods, parameters, and return values.

```json
{
  "version" : 1,
  "kind" : "dev",
  "author" : "Larry A. Gardner",
  "details" : "All function calls are currently implemented without side effects",
  "custom:experimental" : "This is an experimental contract.",
  "methods" :
  {
    "age(uint256)" :
    {
      "details" : "The Alexandr N. Tetearing algorithm could increase precision",
      "params" : 
      {
        "rings" : "The number of rings from dendrochronological sample"
      },
      "returns" : { 
        "_0" : "Age in years, rounded up for partial years",
        "_1" : "Name of the tree"
      }
    },
    "leaves()" :
    {
        "details" : "Returns only a fixed number."
    }
  },
  "title" : "A simulator for trees"
}

```

--------------------------------

### Generated Source Files Reference

Source: https://docs.soliditylang.org/en/v0.8.30/internals/source_mappings

Indicates how to retrieve internally generated source files and their identifiers, which are referenced in source mappings but not part of the original input.

```json
`output['contracts'][sourceName][contractName]['evm']['bytecode']['generatedSources']`
```

--------------------------------

### Solidity Compound and Increment/Decrement Operators

Source: https://docs.soliditylang.org/en/v0.8.30/types

Illustrates the shorthand compound assignment operators (+=, -=, etc.) and the increment/decrement operators (++a, a++, --a, a--) in Solidity. It explains their equivalence to standard operations and the difference in return values for pre/post increment/decrement.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

contract OperatorExamples {
    uint public counter = 5;

    function compoundAssignment() public {
        uint a = 10;
        a += 5; // a is now 15
        counter *= 2; // counter is now 10
    }

    function incrementDecrement() public returns (uint, uint) {
        uint preIncrement = ++counter; // counter is 11, preIncrement is 11
        uint postIncrement = counter++; // postIncrement is 11, counter is 12
        uint preDecrement = --counter; // counter is 11, preDecrement is 11
        uint postDecrement = counter--; // postDecrement is 11, counter is 10
        return (postIncrement, postDecrement);
    }
}
```

--------------------------------

### Disable SMT Tests

Source: https://docs.soliditylang.org/en/v0.8.30/contributing

Skips SMT (Satisfiability Modulo Theories) tests, which require `z3` or `Eldarica` executables. This is useful if these dependencies are not available.

```shell
export SMT_FLAGS=--no-smt
./scripts/tests.sh
```

```shell
./scripts/soltest.sh --no-smt
```

--------------------------------

### Solidity Logging (log0-log4)

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Emits log events with up to four topics. `log0` emits a log with no topics, while `log1` to `log4` include a specified number of indexed topics along with arbitrary data.

```Solidity
log0(memory_pointer, data_size);
log1(memory_pointer, data_size, topic1);
log2(memory_pointer, data_size, topic1, topic2);
log3(memory_pointer, data_size, topic1, topic2, topic3);
log4(memory_pointer, data_size, topic1, topic2, topic3, topic4);
```

--------------------------------

### Solidity B Storage Layout

Source: https://docs.soliditylang.org/en/v0.8.30/internals/layout_in_storage

Demonstrates the storage layout for a Solidity contract 'B', highlighting the packing of smaller data types into storage slots.

```Solidity
00 [eeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee]
01 [ffffffffffffffffffffffffffffffff]
02 [                            hhgg]
03 [                           yxxxx]
04 [                               k]
```

--------------------------------

### Solidity: Interact with contracts using abi.encodeWithSignature and call

Source: https://docs.soliditylang.org/en/v0.8.30/types

Shows how to interact with contracts that may not adhere to the ABI or for more control over encoding using 'call'. It uses 'abi.encodeWithSignature' to encode function calls and 'call' to execute them, returning a success boolean and data. State changes are possible, so caution is advised when calling unknown contracts.

```Solidity
bytes memory payload = abi.encodeWithSignature("register(string)", "MyName");
(bool success, bytes memory returnData) = address(nameReg).call(payload);
require(success);
```

--------------------------------

### Solidity: Test with no expected errors

Source: https://docs.soliditylang.org/en/v0.8.30/contributing

This Solidity code snippet represents a valid contract that is expected to compile without any errors or warnings. The absence of the `// ----` separator and subsequent comments indicates a successful compilation.

```solidity
contract test {
    uint256 variable;
}

```

--------------------------------

### Solidity Optimizer Configuration

Source: https://docs.soliditylang.org/en/v0.8.30/using-the-compiler

Configures various optimization techniques for the Solidity compiler. These options are primarily opcode-based or codegen-based and can significantly impact code size and execution efficiency. Defaults are often true when optimization is enabled.

```json
{
        "inliner": false,
        "jumpdestRemover": true,
        "orderLiterals": false,
        "deduplicate": false,
        "cse": false,
        "constantOptimizer": false,
        "simpleCounterForLoopUncheckedIncrement": true,
        "yul": false,
        "yulDetails": {
          "stackAllocation": true,
          "optimizerSteps": "dhfoDgvulfnTUtnIf..."
        }
      }
```

--------------------------------

### Solidity Mapping with Named Parameters

Source: https://docs.soliditylang.org/en/v0.8.30/types

Illustrates a Solidity mapping declaration where key and value names are explicitly provided in the syntax, such as `mapping(address user => uint balance)`. This primarily affects ABI encoding for the getter function's parameters and return values.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.18;

contract MappingExampleWithNames {
    mapping(address user => uint balance) public balances;

    function update(uint newBalance) public {
        balances[msg.sender] = newBalance;
    }
}

```

--------------------------------

### Contract Creation Transaction Payload

Source: https://docs.soliditylang.org/en/v0.8.30/introduction-to-smart-contracts

Explains that contract creation transactions send EVM bytecode as payload, which is then executed to store the contract's code. The output of this execution becomes the contract's permanent code.

```EVM Assembly
// Example: Simplified representation of bytecode returned by contract creation
// In reality, this would be compiled EVM bytecode
PUSH1 0x80 // Load offset for init code
PUSH1 0x40 // Load memory end pointer
MSTORE // Store memory pointer
...
// Contract's runtime bytecode follows init code
STOP
```

--------------------------------

### Disallowed Remappings with Empty Prefix (Solidity)

Source: https://docs.soliditylang.org/en/v0.8.30/050-breaking-changes

Solidity now disallows remappings that use an empty prefix in the `remapings.txt` file or on the command line. This enforces a structured approach to import path resolution.

```INI
# remappings.txt
# This is disallowed:
# =github.com/OpenZeppelin/openzeppelin-contracts/

# This is allowed:
# Openzeppelin/=github.com/OpenZeppelin/openzeppelin-contracts/
```

--------------------------------

### ABI Encoding for bar(bytes3[2])

Source: https://docs.soliditylang.org/en/v0.8.30/abi-spec

Demonstrates the ABI encoding for calling the 'bar' function with a byte array argument. It shows the method ID and how the byte array is padded and included in the encoded data.

```hex
0xfce353f661626300000000000000000000000000000000000000000000000000000000006465660000000000000000000000000000000000000000000000000000000000
```

--------------------------------

### Fixed-Size Byte Array Operations

Source: https://docs.soliditylang.org/en/v0.8.30/types

Illustrates the usage of fixed-size byte arrays (`bytes1` to `bytes32`) in Solidity, including comparison operators, bitwise operators, shift operators, and index access. It also covers the `.length` member and notes on padding for `bytes1[]` and historical changes to the `byte` alias.

```Solidity
pragma solidity ^0.8.30;

contract ByteArrayOps {
    function byteArrayExamples(bytes32 _a, bytes32 _b) public pure returns (bool, bytes32, bytes32, byte) {
        // Comparisons
        bool isEqual = (_a == _b);
        
        // Bitwise operators
        bytes32 bitwiseOr = _a | _b;
        bytes32 bitwiseXor = _a ^ _b;
        bytes32 bitwiseNot = ~_a;

        // Shift operators
        uint8 shiftAmount = 4;
        bytes32 leftShifted = _a << shiftAmount;
        bytes32 rightShifted = _a >> shiftAmount;

        // Index access
        byte firstByte = _a[0];
        
        return (isEqual, bitwiseOr, leftShifted, firstByte);
    }

    function getLength(bytes10 _arr) public pure returns (uint256) {
        return _arr.length;
    }
}
```

--------------------------------

### Solidity Compiler Output Structure

Source: https://docs.soliditylang.org/en/v0.8.30/using-the-compiler

This JSON structure represents the complete output from the Solidity compiler. It includes potential errors, source file analysis (AST), and contract-level details such as ABI, metadata, bytecode, and documentation.

```JSON
{
  "errors": [
    {
      "sourceLocation": {
        "file": "sourceFile.sol",
        "start": 0,
        "end": 100
      },
      "secondarySourceLocations": [
        {
          "file": "sourceFile.sol",
          "start": 64,
          "end": 92,
          "message": "Other declaration is here:"
        }
      ],
      "type": "TypeError",
      "component": "general",
      "severity": "error",
      "errorCode": "3141",
      "message": "Invalid keyword",
      "formattedMessage": "sourceFile.sol:100: Invalid keyword"
    }
  ],
  "sources": {
    "sourceFile.sol": {
      "id": 1,
      "ast": {}
    }
  },
  "contracts": {
    "sourceFile.sol": {
      "ContractName": {
        "abi": [],
        "metadata": "{/* ... */}",
        "userdoc": {},
        "devdoc": {},
        "ir": "",
        "irAst":  {/* ... */},
        "irOptimized": "",
        "irOptimizedAst": {/* ... */},
        "storageLayout": {"storage": [/* ... */], "types": {/* ... */} },
        "transientStorageLayout": {"storage": [/* ... */], "types": {/* ... */} },
        "evm": {
          "assembly": "",
          "legacyAssembly": {},
          "bytecode": {
            "functionDebugData": {
              "@mint_13": {
                "entryPoint": 128,
                "id": 13,
                "parameterSlots": 2,
                "returnSlots": 1
              }
            },
            "object": "00fe",
            "opcodes": "",
            "sourceMap": "",
            "generatedSources": [
              {
                "ast": {/* ... */},
                "contents":"{ function abi_decode(start, end) -> data { data := calldataload(start) } }",
                "id": 2,
                "language": "Yul",
                "name": "#utility.yul"
              }
            ],
            "linkReferences": {
              "libraryFile.sol": {
                "Library1": [

```

--------------------------------

### Solidity Yul: Switch Statement for Multi-way Branching

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Illustrates the 'switch' statement in Yul for comparing an expression against literal constants. It includes a 'default' case for unmatched values. Control flow does not fall through to the next case.

```Solidity Yul
{
    let x := 0
    switch calldataload(4)
    case 0 {
        x := calldataload(0x24)
    }
    default {
        x := calldataload(0x44)
    }
    sstore(0, div(x, 2))
}

```

--------------------------------

### Select Model Checker Engine (JSON)

Source: https://docs.soliditylang.org/en/v0.8.30/smtchecker

Configures the model checking engine within a JSON settings file. Similar to the CLI option, it allows specifying 'all', 'bmc', 'chc', or 'none' for the 'settings.modelChecker.engine' parameter.

```json
settings.modelChecker.engine={all,bmc,chc,none}
```

--------------------------------

### BigInt Library: Helper Functions (Solidity)

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Provides helper functions for the BigInt library: 'limb' to safely access BigInt limbs and 'max' to determine the maximum of two unsigned integers.

```Solidity
function limb(bigint memory a, uint index) internal pure returns (uint) {
        return index < a.limbs.length ? a.limbs[index] : 0;
    }

    function max(uint a, uint b) private pure returns (uint) {
        return a > b ? a : b;
    }
```

--------------------------------

### Metadata Hash Encoding in Bytecode

Source: https://docs.soliditylang.org/en/v0.8.30/metadata

Illustrates the JSON structure appended to the end of Solidity bytecode, containing hashes for IPFS or Swarm, experimental flags, and the compiler version. This allows verification of the contract's metadata.

```json
{
  "ipfs": "<metadata hash>",
  "bzzr1": "<metadata hash>",
  "bzzr0": "<metadata hash>",
  "experimental": true,
  "solc": "<compiler version>"
}
```

--------------------------------

### Solidity Custom Error with revert and require

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Demonstrates defining and using a custom error `InsufficientBalance` with both the `revert` statement and the `require` function in Solidity. This approach provides gas efficiency and clear error messages.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.27;

/// Insufficient balance for transfer. Needed `required` but only
/// `available` available.
/// @param available balance available.
/// @param required requested amount to transfer.
error InsufficientBalance(uint256 available, uint256 required);

contract TestToken {
    mapping(address => uint) balance;
    function transferWithRevertError(address to, uint256 amount) public {
        if (amount > balance[msg.sender])
            revert InsufficientBalance({
                available: balance[msg.sender],
                required: amount
            });
        balance[msg.sender] -= amount;
        balance[to] += amount;
    }
    function transferWithRequireError(address to, uint256 amount) public {
        require(amount <= balance[msg.sender], InsufficientBalance(balance[msg.sender], amount));
        balance[msg.sender] -= amount;
        balance[to] += amount;
    }
    // ...
}

```

--------------------------------

### Solidity bytes and string Concatenation

Source: https://docs.soliditylang.org/en/v0.8.30/cheatsheet

Demonstrates the `concat` function available for `bytes` and `string` types, allowing for the joining of multiple arguments into a single byte array or string.

```Solidity
bytes.concat(...) returns (bytes memory)
```

```Solidity
string.concat(...) returns (string memory)
```

--------------------------------

### Command-Line Interface Standard Input Usage (Solidity Compiler)

Source: https://docs.soliditylang.org/en/v0.8.30/050-breaking-changes

The Solidity compiler's command-line interface (CLI) now mandates the use of `-` when the standard input is used as the source file. This ensures clarity and prevents ambiguity regarding input sources.

```Shell
# Compiling a Solidity file from standard input
solc --optimize --bin - < MyContract.sol

# Previously, this might have worked without -
# solc --optimize --bin MyContract.sol (if MyContract.sol was piped to stdin)
```

--------------------------------

### Solidity Minter Getter Function

Source: https://docs.soliditylang.org/en/v0.8.30/introduction-to-smart-contracts

The automatically generated getter function for the 'minter' state variable in the Solidity 'Coin' contract. This function allows external access to the contract creator's address.

```solidity
function minter() external view returns (address) { return minter; }

```

--------------------------------

### Solidity Contract Assembly Output

Source: https://docs.soliditylang.org/en/v0.8.30/analysing-compilation-output

The raw EVM assembly code generated by the Solidity compiler for the 'C' contract. This output includes constructor logic, deployment code, and metadata.

```assembly
======= contract.sol:C =======
EVM assembly:
    /* "contract.sol":0:86  contract C {... */
  mstore(0x40, 0x80)
  callvalue
  dup1
  iszero
  tag_1
  jumpi
  0x00
  dup1
  revert
tag_1:
  pop
  dataSize(sub_0)
  dup1
  dataOffset(sub_0)
  0x00
  codecopy
  0x00
  return
stop

sub_0: assembly {
        /* "contract.sol":0:86  contract C {... */
      mstore(0x40, 0x80)
      callvalue
      dup1
      iszero
      tag_1
      jumpi
      0x00
      dup1
      revert
    tag_1:
      pop
      jumpi(tag_2, lt(calldatasize, 0x04))
      shr(0xe0, calldataload(0x00))
      dup1
      0x901717d1
      eq
      tag_3
      jumpi
    tag_2:
      0x00
      dup1
      revert
        /* "contract.sol":17:84  function one() public pure returns (uint) {... */
    tag_3:
      tag_4
      tag_5
      jump  // in
    tag_4:
      mload(0x40)
      tag_6
      swap2
      swap1
      tag_7
      jump  // in
    tag_6:
      mload(0x40)
      dup1
      swap2
      sub
      swap1
      return
    tag_5:
        /* "contract.sol":53:57  uint */
      0x00
        /* "contract.sol":76:77  1 */
      0x01
        /* "contract.sol":69:77  return 1 */
      swap1
      pop
        /* "contract.sol":17:84  function one() public pure returns (uint) {... */
      swap1
      jump  // out
        /* "#utility.yul":7:125   */
    tag_10:
        /* "#utility.yul":94:118   */
      tag_12
        /* "#utility.yul":112:117   */
      dup2
        /* "#utility.yul":94:118   */
      tag_13
      jump  // in
    tag_12:
        /* "#utility.yul":89:92   */
      dup3
        /* "#utility.yul":82:119   */
      mstore
        /* "#utility.yul":72:125   */
      pop
      pop
      jump  // out
        /* "#utility.yul":131:353   */
    tag_7:
      0x00
        /* "#utility.yul":262:264   */
      0x20
        /* "#utility.yul":251:260   */
      dup3
        /* "#utility.yul":247:265   */
      add
        /* "#utility.yul":239:265   */
      swap1
      pop
        /* "#utility.yul":275:346   */
      tag_15
        /* "#utility.yul":343:344   */
      0x00
        /* "#utility.yul":332:341   */
      dup4
        /* "#utility.yul":328:345   */
      add
        /* "#utility.yul":319:325   */
      dup5
        /* "#utility.yul":275:346   */
      tag_10
      jump  // in
    tag_15:
        /* "#utility.yul":229:353   */
      swap3
      swap2
      pop
      pop
      jump  // out
        /* "#utility.yul":359:436   */
    tag_13:
      0x00
        /* "#utility.yul":425:430   */
      dup2
        /* "#utility.yul":414:430   */
      swap1
      pop
        /* "#utility.yul":404:436   */
      swap2
      swap1
      pop
      jump  // out

auxdata: 0xa2646970667358221220a5874f19737ddd4c5d77ace1619e5160c67b3d4bedac75fce908fed32d98899864736f6c637827302e382e342d646576656c6f702e323032312e332e33302b636f6d6d69742e65613065363933380058
}

```

--------------------------------

### Solidity Send Function with Insufficient Balance Check

Source: https://docs.soliditylang.org/en/v0.8.30/introduction-to-smart-contracts

Shows a `send` function in Solidity for transferring tokens. It checks if the sender has sufficient balance using an `if` condition and reverts with an `InsufficientBalance` error if not.

```solidity
pragma solidity ^0.8.30;

contract Token {
    mapping(address => uint) public balances;

    // Assume mint function exists and tokens are distributed

    error InsufficientBalance(uint requested, uint available);

    function send(address receiver, uint amount) public {
        if (balances[msg.sender] < amount) {
            revert InsufficientBalance(amount, balances[msg.sender]);
        }
        balances[msg.sender] -= amount;
        balances[receiver] += amount;
    }
}
```

--------------------------------

### Solidity Contract for Multiplication with Transient Storage

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

A simple Solidity contract demonstrating the use of transient storage for a multiplier. This contract can be used to illustrate how transient storage can affect composability across multiple calls within a transaction.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.28;

contract MulService {
    uint transient multiplier;
    function setMultiplier(uint mul) external {
        multiplier = mul;
    }

    function multiply(uint value) external view returns (uint) {
        return value * multiplier;
    }

}
```

--------------------------------

### Solidity Time Unit Conversions

Source: https://docs.soliditylang.org/en/v0.8.30/units-and-global-variables

Illustrates the usage of time unit suffixes (seconds, minutes, hours, days, weeks) in Solidity for time-related calculations. Seconds are the base unit, with defined equivalencies.

```solidity
function f(uint start, uint daysAfter) public {
    if (block.timestamp >= start + daysAfter * 1 days) {
        // ...
    }
}
```

--------------------------------

### Library Address Placeholders in Unlinked Binaries (Solidity)

Source: https://docs.soliditylang.org/en/v0.8.30/050-breaking-changes

In unlinked binary hex files, library address placeholders are now the first 36 hex characters of the keccak256 hash of the fully qualified library name, enclosed in `$...$`. This change reduces placeholder collisions and improves security.

```Hexadecimal
// Example of an unlinked binary placeholder (illustrative)
// Old format: $MyLibrary$
// New format: $Keccak256HashOfFullyQualifiedName_First36Chars$

// The binary file will also contain a mapping from these placeholders to the actual library names.
```

--------------------------------

### Combine Equivalent Functions (Solidity)

Source: https://docs.soliditylang.org/en/v0.8.30/internals/optimizer

This component identifies syntactically equivalent functions (allowing variable renaming but not reordering) and replaces references to one with the other. The actual function removal is handled by UnusedPruner.

--------------------------------

### Define and Use Pre-0.5.0 Library in New Contract

Source: https://docs.soliditylang.org/en/v0.8.30/050-breaking-changes

This snippet illustrates how to use a Solidity library deployed with a version prior to 0.5.0 within a newer contract. It involves defining the library's functions without implementation in the newer contract and linking the address of the pre-0.5.0 library during compilation or deployment.

```solidity
// This will not compile after 0.6.0
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.5.0;

library OldLibrary {
    function someFunction(uint8 a) public returns(bool);
}

contract NewContract {
    function f(uint8 a) public returns (bool) {
        return OldLibrary.someFunction(a);
    }
}
```

--------------------------------

### SMTChecker for Formal Verification (Solidity Compiler)

Source: https://docs.soliditylang.org/en/v0.8.30/050-breaking-changes

The `--formal` command-line option for formal verification in the Solidity compiler has been removed in favor of the `pragma experimental SMTChecker;` directive. This enables the SMTChecker module for formal verification purposes.

```Solidity
pragma solidity ^0.8.30;

// Enable SMTChecker for formal verification
pragma experimental SMTChecker;

contract VerificationTarget {
    // Contract logic to be formally verified
    function checkInvariant() public pure returns (bool) {
        return true;
    }
}
```

--------------------------------

### Source File Identifier Reference

Source: https://docs.soliditylang.org/en/v0.8.30/internals/source_mappings

Shows how to access the unique identifier for a source file from the compiler's standard-JSON output.

```json
`output['sources'][sourceName]['id']`
```

--------------------------------

### Specify Analyzed Contracts for SMTChecker

Source: https://docs.soliditylang.org/en/v0.8.30/smtchecker

Allows users to specify which contracts should be analyzed as the deployed version, optimizing the SMTChecker's analysis by reducing complexity for inheritance hierarchies. This is configured using source:contract pairs in the CLI or a structured object in JSON.

```bash
--model-checker-contracts "<source1.sol:contract1>,<source2.sol:contract2>,<source2.sol:contract3>"
```

```json
"settings.modelChecker.contracts": {
    "source1.sol": ["contract1"],
    "source2.sol": ["contract2", "contract3"]
}
```

--------------------------------

### Solidity Yul: Type Declarations and Multiple Assignments

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Illustrates declaring variables with explicit types (though commented as not yet implemented) and assigning multiple values from function calls in Yul. Note: The type annotations shown are for illustrative purposes and may not be supported in current compilers.

```Solidity Yul
// This will not compile (u32 and u256 type not implemented yet)
{
    let zero:u32 := 0:u32
    let v:u256, t:u32 := f() // Assuming f() returns two values
    let x, y := g() // Assuming g() returns two values
}

```

--------------------------------

### Solidity Caller Contract for Fallback Functions

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

A Solidity contract demonstrating how to call fallback functions in other contracts. It shows calling a non-payable fallback and interacting with a payable fallback and receive function using low-level calls.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.2 <0.9.0;

contract Caller {
    function callTest(Test test) public returns (bool) {
        (bool success,) = address(test).call(abi.encodeWithSignature("nonExistingFunction()"));
        require(success);
        // results in test.x becoming == 1.

        // address(test) will not allow to call ``send`` directly, since ``test`` has no payable
        // fallback function.
        // It has to be converted to the ``address payable`` type to even allow calling ``send`` on it.
        address payable testPayable = payable(address(test));

        // If someone sends Ether to that contract,
        // the transfer will fail, i.e. this returns false here.
        return testPayable.send(2 ether);
    }

    function callTestPayable(TestPayable test) public returns (bool) {
        (bool success,) = address(test).call(abi.encodeWithSignature("nonExistingFunction()"));
        require(success);
        // results in test.x becoming == 1 and test.y becoming 0.
        (success,) = address(test).call{value: 1}(abi.encodeWithSignature("nonExistingFunction()"));
        require(success);
        // results in test.x becoming == 1 and test.y becoming 1.

        // If someone sends Ether to that contract, the receive function in TestPayable will be called.
        // Since that function writes to storage, it takes more gas than is available with a
        // simple ``send`` or ``transfer``. Because of that, we have to use a low-level call.
        (success,) = address(test).call{value: 2 ether}("");
        require(success);
        // results in test.x becoming == 2 and test.y becoming 2 ether.

        return true;
    }
}
```

--------------------------------

### Solidity Mathematical and Cryptographic Functions

Source: https://docs.soliditylang.org/en/v0.8.30/cheatsheet

Offers built-in functions for common mathematical operations like addition and multiplication modulo a number, as well as cryptographic hashing (Keccak-256, SHA-256, RIPEMD-160) and elliptic curve signature recovery.

```Solidity
bytes32 hash = keccak256(abi.encodePacked(data));
uint result = addmod(a, b, k);
```

--------------------------------

### Solidity: Function Returning Multiple Variables Directly

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Illustrates how to return multiple values directly from a Solidity function using the 'return' statement with a tuple. This method bypasses the need for explicitly naming and assigning to return variables.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract Simple {
    function arithmetic(uint a, uint b)
        public
        pure
        returns (uint sum, uint product)
    {
        return (a + b, a * b);
    }
}

```

--------------------------------

### EVM Dialect Storage Operations

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Handles interactions with the EVM's persistent storage. 'sload' reads a value from a storage slot, and 'sstore' writes a value to a storage slot. 'tload' and 'tstore' are used for transient storage.

```solidity
sload(p)
sstore(p, v)
tload(p)
tstore(p, v)
```

--------------------------------

### For Loop Condition Transformation

Source: https://docs.soliditylang.org/en/v0.8.30/internals/optimizer

Moves a for loop's iteration condition into the loop body, transforming `for { Init } C { Post } { Body }` to `for { Init } 1 { Post } { if iszero(C) { break } Body }`. This is useful for applying optimizations like LoopInvariantCodeMotion to the condition.

```solidity
for { Init... } C { Post... } {
    Body...
}

is transformed to

for { Init... } 1 { Post... } {
    if iszero(C) { break }
    Body...
}
```

--------------------------------

### Solidity Payable Fallback and Receive Functions

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Illustrates a Solidity contract with both a payable fallback function and a receive function. The fallback handles calls with data, while the receive function specifically handles plain Ether transfers (calls with empty calldata).

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.2 <0.9.0;

contract TestPayable {
    uint x;
    uint y;
    // This function is called for all messages sent to
    // this contract, except plain Ether transfers
    // (there is no other function except the receive function).
    // Any call with non-empty calldata to this contract will execute
    // the fallback function (even if Ether is sent along with the call).
    fallback() external payable { x = 1; y = msg.value; }

    // This function is called for plain Ether transfers, i.e.
    // for every call with empty calldata.
    receive() external payable { x = 2; y = msg.value; }
}
```

--------------------------------

### BigInt Library: Add Functionality (Solidity)

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Implements addition for BigInt numbers, handling carries and potential limb expansion. It requires a 'limb' helper function and a 'max' helper function.

```Solidity
function add(bigint memory a, bigint memory b) internal pure returns (bigint memory r) {
        r.limbs = new uint[](max(a.limbs.length, b.limbs.length));
        uint carry = 0;
        for (uint i = 0; i < r.limbs.length; ++i) {
            uint limbA = limb(a, i);
            uint limbB = limb(b, i);
            unchecked {
                r.limbs[i] = limbA + limbB + carry;

                if (limbA + limbB < limbA || (limbA + limbB == type(uint).max && carry > 0))
                    carry = 1;
                else
                    carry = 0;
            }
        }
        if (carry > 0) {
            // too bad, we have to add a limb
            uint[] memory newLimbs = new uint[](r.limbs.length + 1);
            uint i;
            for (i = 0; i < r.limbs.length; ++i)
                newLimbs[i] = r.limbs[i];
            newLimbs[i] = carry;
            r.limbs = newLimbs;
        }
    }
```

--------------------------------

### Solidity: External Function Types for Contract Interaction (Oracle Pattern)

Source: https://docs.soliditylang.org/en/v0.8.30/types

Demonstrates using external function types for callback mechanisms in smart contracts. It includes an Oracle contract that accepts data and a callback function, and an OracleUser contract that queries the Oracle and handles the response.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.22 <0.9.0;


contract Oracle {
    struct Request {
        bytes data;
        function(uint) external callback;
    }

    Request[] private requests;
    event NewRequest(uint);

    function query(bytes memory data, function(uint) external callback) public {
        requests.push(Request(data, callback));
        emit NewRequest(requests.length - 1);
    }

    function reply(uint requestID, uint response) public {
        // Here goes the check that the reply comes from a trusted source
        requests[requestID].callback(response);
    }
}


contract OracleUser {
    Oracle constant private ORACLE_CONST = Oracle(address(0x00000000219ab540356cBB839Cbe05303d7705Fa)); // known contract
    uint private exchangeRate;

    function buySomething() public {
        ORACLE_CONST.query("USD", this.oracleResponse);
    }

    function oracleResponse(uint response) public {
        require(
            msg.sender == address(ORACLE_CONST),
            "Only oracle can call this."
        );
        exchangeRate = response;
    }
}

```

--------------------------------

### EVM Dialect System Opcodes

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Core system-level operations. 'stop' halts execution, 'gas' returns the remaining gas, and 'keccak256' computes the Keccak-256 hash of a memory region. 'pop' discards a value.

```solidity
stop()
gas()
keccak256(p, n)
pop(x)
```

--------------------------------

### Solidity Validations and Assertions

Source: https://docs.soliditylang.org/en/v0.8.30/cheatsheet

Provides functions to validate conditions and revert execution if a condition is false. `require` is used for input validation and external conditions, while `assert` is for internal errors. `revert` allows custom error messages.

```Solidity
require(msg.value > 0, "Must send some Ether");
assert(balance >= amount);
```

--------------------------------

### Solidity Linker Symbol Usage

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Demonstrates the usage of the `linkersymbol` function in Yul to specify a placeholder for a library address that will be substituted by the linker. It requires a string literal argument representing the library identifier.

```Yul
let a := linkersymbol("file.sol:Math")
```

--------------------------------

### Solidity Contract for Tuple Type Demonstration

Source: https://docs.soliditylang.org/en/v0.8.30/abi-spec

This Solidity code defines a contract with structs and functions that utilize tuple types, demonstrating how these are handled by the ABI encoder. It requires the 'abicoder v2' pragma.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.5 <0.9.0;
pragma abicoder v2;

contract Test {
    struct S { uint a; uint[] b; T[] c; }
    struct T { uint x; uint y; }
    function f(S memory, T memory, uint) public pure {}
    function g() public pure returns (S memory, T memory, uint) {}
}

```

--------------------------------

### Yul Object Grammar

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Defines the syntax for Yul objects, specifying how code and data sections are structured and how hex literals and string literals are used for data encoding.

```yul
Object = 'object' StringLiteral '{' Code ( Object | Data )* '}'
Code = 'code' Block
Data = 'data' StringLiteral ( HexLiteral | StringLiteral )
HexLiteral = 'hex' ('"' ([0-9a-fA-F]{2})* '"' | '\'' ([0-9a-fA-F]{2})* '\'')
StringLiteral = '"' ([^"\r\n\\] | '\\' .)* '"'
```

--------------------------------

### Expression Splitter Transformation

Source: https://docs.soliditylang.org/en/v0.8.30/internals/optimizer

Illustrates the Expression Splitter's function in transforming nested expressions into a sequence of assignments to unique variables. This ensures each function call receives only variables as arguments.

```solidity
{
    let _1 := 0x20
    let _2 := 0x456
    let _3 := mload(_2)
    let _4 := mul(_3, _1)
    let _5 := 0x123
    let _6 := mload(_5)
    let z := add(_6, _4)
}
```

--------------------------------

### Solidity: Use delegatecall for library code

Source: https://docs.soliditylang.org/en/v0.8.30/types

Explains 'delegatecall' for using library code from another contract. It executes the target contract's code within the context of the calling contract, preserving storage and balance. Careful consideration of storage layout is necessary for safe usage.

--------------------------------

### Solidity Import Statements

Source: https://docs.soliditylang.org/en/v0.8.30/layout-of-source-files

Allows modularization of Solidity code, similar to JavaScript's ES6 modules. It supports importing all global symbols, specific symbols, or renaming imported symbols using aliases.

```solidity
import "filename";

```

```solidity
import * as symbolName from "filename";

```

```solidity
import "filename" as symbolName;

```

```solidity
import {symbol1 as alias, symbol2} from "filename";

```

--------------------------------

### Solidity: Pad End with Zeros on Fixed-Size Bytes Conversion

Source: https://docs.soliditylang.org/en/v0.8.30/types

Demonstrates converting a smaller fixed-size bytes type to a larger one, padding the end with zeros. Accessing bytes within the original range before and after conversion yields the same values.

```solidity
bytes2 a = 0x1234;
bytes4 b = bytes4(a); // b will be 0x12340000
assert(a[0] == b[0]);
assert(a[1] == b[1]);

```

--------------------------------

### Solidity Compiler Command-Line: Error Reporter

Source: https://docs.soliditylang.org/en/v0.8.30/060-breaking-changes

Shows how to switch between the new error reporter (enabled by default) and the deprecated old error reporter using a command-line flag.

```bash
# Use the new error reporter (default)
solc ...

# Fallback to the deprecated old error reporter
solc --old-reporter ...
```

--------------------------------

### Git Rebase for Maintaining Clean History

Source: https://docs.soliditylang.org/en/v0.8.30/contributing

This snippet demonstrates the recommended Git command for integrating upstream changes into a feature branch. Using `git rebase` instead of `git merge` helps maintain a linear and cleaner commit history, making pull request reviews easier.

```git
git rebase develop
```

--------------------------------

### Solidity: Function Returning Multiple Variables by Assignment

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Demonstrates declaring named return variables and assigning values to them within a Solidity function. The function calculates and returns the sum and product of two unsigned integers.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract Simple {
    function arithmetic(uint a, uint b)
        public
        pure
        returns (uint sum, uint product)
    {
        sum = a + b;
        product = a * b;
    }
}

```

--------------------------------

### Filtering Ethereum Logs with web3.js

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

This snippet demonstrates how to use web3.js to subscribe to and filter Ethereum logs based on block number, contract address, and topics. It logs any matching events received.

```javascript
var options = {
    fromBlock: 0,
    address: web3.eth.defaultAccount,
    topics: ["0x0000000000000000000000000000000000000000000000000000000000000000", null, null]
};
web3.eth.subscribe('logs', options, function (error, result) {
    if (!error)
        console.log(result);
})
    .on("data", function (log) {
        console.log(log);
    })
    .on("changed", function (log) {
});

```

--------------------------------

### Solidity Ether Transfer (transfer)

Source: https://docs.soliditylang.org/en/v0.8.30/units-and-global-variables

Sends a specified amount of Wei to an address. This method reverts on failure and forwards a fixed gas stipend of 2300. It is recommended for safe Ether transfers.

```Solidity
payable(someAddress).transfer(amountInWei);
```

--------------------------------

### Show Proved Targets in SMTChecker

Source: https://docs.soliditylang.org/en/v0.8.30/smtchecker

Enables the display of specific proved verification targets. When enabled, the SMTChecker will issue a warning for each engine stating how many targets were proved. This can be controlled via the CLI or JSON configuration.

```bash
--model-checker-show-proved-safe
```

```json
"settings.modelChecker.showProvedSafe": true
```

--------------------------------

### Solidity: RIPEMD160 Hash

Source: https://docs.soliditylang.org/en/v0.8.30/units-and-global-variables

Computes the RIPEMD-160 hash of the input bytes.

```Solidity
ripemd160(bytes memory) returns (bytes20)
```

--------------------------------

### Solidity: NatSpec Constructor and Function Userdoc Consistency

Source: https://docs.soliditylang.org/en/v0.8.30/070-breaking-changes

Ensures consistent userdoc output for constructors and functions in NatSpec comments. This promotes uniformity in documentation generation and improves clarity for users.

```Solidity
/// @notice Constructor for the contract.
/// @custom:oz-custom-Buidl-template "ZeroDev"
constructor() {}

/// @notice Returns a greeting message.
/// @param name The name to greet.
/// @return The greeting string.
function greet(string memory name) public pure returns (string memory) {
    return string(abi.encodePacked("Hello, ", name, "!"));
}
```

--------------------------------

### Solidity Array Initialization and Assignment

Source: https://docs.soliditylang.org/en/v0.8.30/types

Demonstrates initializing a contract with a large array of integers and a dynamic array of boolean pairs. It also shows how to assign a new dynamic array to a storage array, effectively replacing its contents. References to storage arrays can also be used to modify struct members.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

contract ArrayContract {
    uint[2**20] aLotOfIntegers;
    // Note that the following is not a pair of dynamic arrays but a
    // dynamic array of pairs (i.e. of fixed size arrays of length two).
    // In Solidity, T[k] and T[] are always arrays with elements of type T,
    // even if T itself is an array.
    // Because of that, bool[2][] is a dynamic array of elements
    // that are bool[2]. This is different from other languages, like C.
    // Data location for all state variables is storage.
    bool[2][] pairsOfFlags;

    // newPairs is stored in memory
    function setAllFlagPairs(bool[2][] memory newPairs) public {
        // assignment to a storage array performs a copy of ``newPairs`` and
        // replaces the complete array ``pairsOfFlags``.
        pairsOfFlags = newPairs;
    }

    struct StructType {
        uint[] contents;
        uint moreInfo;
    }
    StructType s;

    function f(uint[] memory c) public {
        // stores a reference to ``s`` in ``g``
        StructType storage g = s;
        // also changes ``s.moreInfo``.
        g.moreInfo = 2;
        // assigns a copy because ``g.contents``
        // is not a local variable, but a member of
        // a local variable.
        g.contents = c;
    }

    function setFlagPair(uint index, bool flagA, bool flagB) public {
        // access to a non-existing index will throw an exception
        pairsOfFlags[index][0] = flagA;
        pairsOfFlags[index][1] = flagB;
    }

    // ... other functions ...
}

```

--------------------------------

### Solidity f function with addmod and mulmod argument evaluation

Source: https://docs.soliditylang.org/en/v0.8.30/ir-breaking-changes

Compares the evaluation order of arguments for addmod and mulmod in the f function between old and new code generators. Demonstrates how pre-increment operations affect the results.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.1;
contract C {
    function f() public pure returns (uint256 aMod, uint256 mMod) {
        uint256 x = 3;
        // Old code gen: add/mulmod(5, 4, 3)
        // New code gen: add/mulmod(4, 5, 5)
        aMod = addmod(++x, ++x, x);
        mMod = mulmod(++x, ++x, x);
    }
}
```

--------------------------------

### ABI Encoding for baz(uint32,bool)

Source: https://docs.soliditylang.org/en/v0.8.30/abi-spec

Illustrates the ABI encoding for calling the 'baz' function with a uint32 and a bool. It includes the method ID and how the integer and boolean values are padded to 32 bytes.

```hex
0xcdcd77c00000000000000000000000000000000000000000000000000000000000000045000000000000000000000000000000000000000000000000000000000000001
```

--------------------------------

### Solidity: Type Information for Integer Types

Source: https://docs.soliditylang.org/en/v0.8.30/units-and-global-variables

Provides the minimum and maximum representable values for an integer type `T` using `type(T).min` and `type(T).max` respectively.

```Solidity
type(T).min
type(T).max
```

--------------------------------

### Solidity Immutable Variable Handling (setimmutable, loadimmutable)

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Internal Yul functions used by the Solidity compiler to manage immutable variables. `setimmutable` writes a value to a placeholder in the runtime bytecode, while `loadimmutable` reads the placeholder's value.

```Yul
setimmutable(offset, "variableName", value);
loadimmutable("variableName");
```

--------------------------------

### Show Unsupported Language Features in SMTChecker

Source: https://docs.soliditylang.org/en/v0.8.30/smtchecker

Controls the reporting of unsupported Solidity language features. When enabled, the SMTChecker will report generic warnings for unsupported constructs encountered, potentially causing false positives if properties depend on their precise behavior. This can be configured via CLI or JSON.

```bash
--model-checker-show-unsupported
```

```json
"settings.modelChecker.showUnsupported": true
```

--------------------------------

### Solidity Fixed Point Number Declaration

Source: https://docs.soliditylang.org/en/v0.8.30/types

Demonstrates the declaration syntax for signed and unsigned fixed-point numbers in Solidity, including alias definitions for `ufixed` and `fixed`.

```solidity
fixed / ufixed: Signed and unsigned fixed point number of various sizes.
Keywords `ufixedMxN` and `fixedMxN`, where `M` represents the number of bits taken by the type and `N` represents how many decimal points are available.
`ufixed` and `fixed` are aliases for `ufixed128x18` and `fixed128x18`, respectively.
```

--------------------------------

### Solidity Ether Transfer (send)

Source: https://docs.soliditylang.org/en/v0.8.30/units-and-global-variables

Sends a specified amount of Wei to an address and returns a boolean indicating success or failure. It forwards a fixed gas stipend of 2300 and is not adjustable. Always check the return value due to potential failures.

```Solidity
bool success = payable(someAddress).send(amountInWei);
```

--------------------------------

### C API Changes for libsolc

Source: https://docs.soliditylang.org/en/v0.8.30/060-breaking-changes

Details the modifications to the C API for `libsolc`, including renaming `solidity_free` to `solidity_reset`, adding `solidity_alloc` and `solidity_free`, and requiring explicit freeing of the returned string from `solidity_compile`.

```c
// Renamed function
// solidity_free(memory_block);
// becomes:
solidity_reset(memory_block);

// New functions for memory management
void* solidity_alloc(size_t size);
void solidity_free(void* ptr);

// solidity_compile now returns a string that needs explicit freeing
char* result_string = solidity_compile(...);
// ... use result_string ...
solidity_free(result_string);
```

--------------------------------

### Solidity: Disjoint Scopes with Same Variable Names

Source: https://docs.soliditylang.org/en/v0.8.30/control-structures

Demonstrates how Solidity's scoping rules allow variables with the same name to exist in different blocks without conflict. Each 'same' variable is confined to its respective block.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.5.0 <0.9.0;
contract C {
    function minimalScoping() pure public {
        {
            uint same;
            same = 1;
        }

        {
            uint same;
            same = 3;
        }
    }
}
```

--------------------------------

### Solidity Abstract Contract Definition

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Defines an abstract contract 'Feline' with an unimplemented virtual function 'utterance'. Abstract contracts cannot be instantiated directly and are used as base classes for other contracts.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

abstract contract Feline {
    function utterance() public virtual returns (bytes32);
}
```

--------------------------------

### Solidity Low-Level CALL

Source: https://docs.soliditylang.org/en/v0.8.30/units-and-global-variables

Performs a low-level CALL to an address with a given payload. It forwards all available gas and returns a success status and the return data. Use with caution as it bypasses type checking.

```Solidity
 (bool success, bytes memory returnData) = someAddress.call(payload); 
```

--------------------------------

### Solidity Memory Guard Usage

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Illustrates the `memoryguard` function in Yul, which helps the optimizer by defining memory usage constraints. The caller guarantees memory usage within specified ranges, enabling optimizations like the stack limit evader.

```Yul
let ptr := memoryguard(size)
```

--------------------------------

### Solidity: Type Information for Contracts

Source: https://docs.soliditylang.org/en/v0.8.30/units-and-global-variables

Retrieves information about a contract type using `type(C)`. It provides the contract's name and its creation or runtime bytecode as memory byte arrays. Accessing these properties is restricted to external contracts.

```Solidity
type(C).name
type(C).creationCode
type(C).runtimeCode
```

--------------------------------

### Yul Recursive Exponentiation Function (EVM Dialect)

Source: https://docs.soliditylang.org/en/v0.8.30/yul

A Yul implementation of an exponentiation function using recursion. It defines base cases for exponent 0 and 1, and recursively calls itself for larger exponents, handling odd exponents by multiplying with the base.

```Yul
{
    function power(base, exponent) -> result
    {
        switch exponent
        case 0 { result := 1 }
        case 1 { result := base }
        default
        {
            result := power(mul(base, base), div(exponent, 2))
            switch mod(exponent, 2)
                case 1 { result := mul(base, result) }
        }
    }
}
```

--------------------------------

### Filter Unique Fuzzer Errors

Source: https://docs.soliditylang.org/en/v0.8.30/contributing

A command to process fuzzer reports and filter out unique error-producing source files, helping to manage and analyze the fuzzer's findings.

```bash
scripts/uniqueErrors.sh
```

--------------------------------

### Solidity Compiler Command-Line: Yul Optimizer

Source: https://docs.soliditylang.org/en/v0.8.30/060-breaking-changes

Illustrates the command-line flags for enabling or disabling the Yul optimizer in the Solidity compiler.

```bash
# Enable Yul optimizer (enabled by default with --optimize)
solc --optimize ...

# Disable Yul optimizer specifically
solc --no-optimize-yul ...
```

--------------------------------

### Solidity: Mapping Behavior and Deletion Limitations

Source: https://docs.soliditylang.org/en/v0.8.30/security-considerations

Demonstrates the behavior of mappings within dynamic arrays in Solidity, highlighting that deleting the array does not clear the mapping elements. It shows how to manage mappings and suggests using libraries for proper deletion.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

contract Map {
    mapping(uint => uint)[] array;

    function allocate(uint newMaps) public {
        for (uint i = 0; i < newMaps; i++)
            array.push();
    }

    function writeMap(uint map, uint key, uint value) public {
        array[map][key] = value;
    }

    function readMap(uint map, uint key) public view returns (uint) {
        return array[map][key];
    }

    function eraseMaps() public {
        delete array;
    }
}

```

--------------------------------

### EVM Dialect Contract Information Opcodes

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Provides access to information about the current execution context and the contract itself. This includes the current address, balance, caller information, call value, gas available, and details about the call data.

```solidity
address()
balance(a)
selfbalance()
caller()
callvalue()
calldataload(p)
calldatasize()
```

--------------------------------

### Solidity Combined Function Call Syntax

Source: https://docs.soliditylang.org/en/v0.8.30/080-breaking-changes

Demonstrates the updated syntax for making function calls in Solidity with options like gas and value. Multiple options are now comma-separated within a single `{}` block.

```Solidity
c.f{gas: 10000, value: 1}()
```

--------------------------------

### Solidity Function Definition and External Helper

Source: https://docs.soliditylang.org/en/v0.8.30/structure-of-a-contract

Defines a public, payable function 'bid' within a contract and a pure helper function 'helper' outside a contract. Functions are executable units of code, accepting parameters and returning values.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.1 <0.9.0;

contract SimpleAuction {
    function bid() public payable { // Function
        // ...
    }
}

// Helper function defined outside of a contract
function helper(uint x) pure returns (uint) {
    return x * 2;
}

```

--------------------------------

### Solidity: Revert Functions

Source: https://docs.soliditylang.org/en/v0.8.30/units-and-global-variables

Aborts execution and reverts state changes. Can include an explanatory string reason.

```Solidity
revert()
revert(string memory reason)
```

--------------------------------

### Allocate Dynamic Memory Arrays in Solidity

Source: https://docs.soliditylang.org/en/v0.8.30/types

Demonstrates allocating dynamic memory arrays of specified lengths using the 'new' operator. Supports uint and bytes arrays. Note: Memory arrays cannot be resized after allocation.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract C {
    function f(uint len) public pure {
        uint[] memory a = new uint[](7);
        bytes memory b = new bytes(len);
        assert(a.length == 7);
        assert(b.length == len);
        a[6] = 8;
    }
}

```

--------------------------------

### Solidity Compiler Error Types

Source: https://docs.soliditylang.org/en/v0.8.30/using-the-compiler

Lists and describes various error types that can occur during Solidity compilation, categorized from JSON and IO errors to specific language and type system issues.

```text
1. `JSONError`: JSON input doesn’t conform to the required format, e.g. input is not a JSON object, the language is not supported, etc.
2. `IOError`: IO and import processing errors, such as unresolvable URL or hash mismatch in supplied sources.
3. `ParserError`: Source code doesn’t conform to the language rules.
4. `DocstringParsingError`: The NatSpec tags in the comment block cannot be parsed.
5. `SyntaxError`: Syntactical error, such as `continue` is used outside of a `for` loop.
6. `DeclarationError`: Invalid, unresolvable or clashing identifier names. e.g. `Identifier not found`
7. `TypeError`: Error within the type system, such as invalid type conversions, invalid assignments, etc.
8. `UnimplementedFeatureError`: Feature is not supported by the compiler, but is expected to be supported in future versions.
9. `InternalCompilerError`: Internal bug triggered in the compiler - this should be reported as an issue.
10. `Exception`: Unknown failure during compilation - this should be reported as an issue.
11. `CompilerError`: Invalid use of the compiler stack - this should be reported as an issue.
12. `FatalError`: Fatal error not processed correctly - this should be reported as an issue.
13. `YulException`: Error during Yul code generation - this should be reported as an issue.
14. `Warning`: A warning, which didn’t stop the compilation, but should be addressed if possible.
15. `Info`: Information that the compiler thinks the user might find useful, but is not dangerous and does not necessarily need to be addressed.
```

--------------------------------

### Solidity External Contract Call with Value and Gas

Source: https://docs.soliditylang.org/en/v0.8.30/control-structures

Demonstrates calling a function on another contract, specifying Ether value and gas. The 'payable' modifier is necessary for functions receiving Ether. Note that `feed.info{value: 10, gas: 800}` sets options, and `()` executes the call.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.2 <0.9.0;

contract InfoFeed {
    function info() public payable returns (uint ret) { return 42; }
}

contract Consumer {
    InfoFeed feed;
    function setFeed(InfoFeed addr) public { feed = addr; }
    function callFeed() public { feed.info{value: 10, gas: 800}(); }

}
```

--------------------------------

### Solidity Address Type Members

Source: https://docs.soliditylang.org/en/v0.8.30/cheatsheet

Details the properties and low-level interaction functions available for the `address` type in Solidity. This includes accessing balance, code, codehash, and performing low-level calls like `call`, `delegatecall`, and `staticcall`.

```Solidity
<address>.balance (uint256)
```

```Solidity
<address>.code (bytes memory)
```

```Solidity
<address>.codehash (bytes32)
```

```Solidity
<address>.call(bytes memory) returns (bool, bytes memory)
```

```Solidity
<address>.delegatecall(bytes memory) returns (bool, bytes memory)
```

```Solidity
<address>.staticcall(bytes memory) returns (bool, bytes memory)
```

```Solidity
<address payable>.send(uint256 amount) returns (bool)
```

```Solidity
<address payable>.transfer(uint256 amount)
```

--------------------------------

### EVM Version and IR Compilation

Source: https://docs.soliditylang.org/en/v0.8.30/using-the-compiler

Specifies the target EVM version for compilation and whether to use the Yul Intermediate Representation. The EVM version affects type checking and code generation, supporting various hard fork names. `viaIR` enables Yul IR processing.

```json
{
    "evmVersion": "prague",
    "eofVersion": null,
    "viaIR": true
  }
```

--------------------------------

### Solidity (Pre-0.5.0): Scoping Issue (Will Not Compile)

Source: https://docs.soliditylang.org/en/v0.8.30/control-structures

Shows a code snippet that would compile before Solidity version 0.5.0 but causes an error afterwards due to stricter scoping rules. It highlights the change from JavaScript-like scoping to C99-like scoping.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.5.0 <0.9.0;
// This will not compile
contract C {
    function f() pure public returns (uint) {
        x = 2;
        uint x;
        return x;
    }
}
```

--------------------------------

### Solidity Beacon Chain Randomness (prevrandao)

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Returns the randomness provided by the beacon chain, as specified in EIP-4399. This replaces the old `difficulty` opcode semantics for EVM versions >= Paris.

```Solidity
uint256 randomness = prevrandao();
```

--------------------------------

### EVM Dialect Call Data and Code Operations

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Enables copying data from call data and accessing code information. 'calldatacopy' copies data from the call data to memory. 'codesize', 'codecopy', 'extcodesize', 'extcodecopy', and 'extcodehash' provide information about the contract's own code and the code of other addresses.

```solidity
calldatacopy(t, f, s)
codesize()
codecopy(t, f, s)
extcodesize(a)
extcodecopy(a, t, f, s)
extcodehash(a)
```

--------------------------------

### Solidity: Low-level Ether transfer with send

Source: https://docs.soliditylang.org/en/v0.8.30/types

Explains the 'send' function as a low-level alternative to 'transfer'. Unlike 'transfer', 'send' returns 'false' on failure instead of reverting. It's crucial to check the return value of 'send' due to potential failures related to call stack depth or recipient gas limits.

--------------------------------

### Solidity ABI Encoding Functions

Source: https://docs.soliditylang.org/en/v0.8.30/units-and-global-variables

Encode and decode data according to the Application Binary Interface (ABI) specification in Solidity. Useful for preparing data for external calls or parsing received data.

```solidity
// Example of ABI encoding and decoding
bytes memory encoded = abi.encode(uint(1), bytes("hello"));
(uint a, bytes memory b) = abi.decode(encoded, (uint, bytes));
```

```solidity
// Example of packed encoding
bytes memory packedData = abi.encodePacked(uint(1), bytes("hello"));
```

```solidity
// Example of encoding with selector
bytes4 selector = bytes4(keccak256(bytes("transfer(address,uint256)")));
bytes memory callData = abi.encodeWithSelector(selector, address(1), 100);
```

--------------------------------

### Solidity Contract Interaction (call)

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Calls another contract at a given address. It allows specifying gas, ether value, input data, and output buffer. Returns 1 on success and 0 on error (e.g., out of gas).

```Solidity
bool success = call(gas, target_address, value, data_ptr, data_size, output_ptr, output_size);
// Example usage:
// (bool success, bytes memory returndata) = target_contract.call{value: msg.value, gas: 100000}(abi.encodeWithSignature("functionName(uint256)", arg1));
```

--------------------------------

### Simulating Shifts with Multiplication/Division in Solidity

Source: https://docs.soliditylang.org/en/v0.8.30/types

Illustrates how bitwise shift operations in Solidity can be emulated using multiplication and division by powers of two. The left operand's type determines the final result's type after truncation.

```Solidity
// Equivalent to x << y
x * (2**y);

// Equivalent to x >> y (rounding towards negative infinity)
x / (2**y);
```

--------------------------------

### EVM Dialect Bitwise and Logical Opcodes

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Encompasses bitwise operations and logical comparisons. These functions allow for bitwise AND, OR, XOR, and NOT, as well as comparisons for less than, greater than, equality, and checking for zero.

```solidity
not(x)
lt(x, y)
gt(x, y)
slt(x, y)
sgt(x, y)
eq(x, y)
iszero(x)
and(x, y)
or(x, y)
xor(x, y)
```

--------------------------------

### Yul Iterative Exponentiation Function (EVM Dialect)

Source: https://docs.soliditylang.org/en/v0.8.30/yul

An iterative implementation of an exponentiation function in Yul using a for-loop. It initializes the result to 1 and repeatedly multiplies it by the base until the exponent counter reaches the specified exponent.

```Yul
{
    function power(base, exponent) -> result
    {
        result := 1
        for { let i := 0 } lt(i, exponent) { i := add(i, 1) }
        {
            result := mul(result, base)
        }
    }
}
```

--------------------------------

### Solidity Address CodeHash

Source: https://docs.soliditylang.org/en/v0.8.30/units-and-global-variables

Returns the keccak256 hash of the bytecode of a contract at a given address.

```Solidity
bytes32 codehash = someAddress.codehash;
```

--------------------------------

### Solidity Smart Contract with Inline Assembly and Bitwise NOT

Source: https://docs.soliditylang.org/en/v0.8.30/ir-breaking-changes

A Solidity smart contract demonstrating the effect of cleanup operations on bitwise NOT and inline assembly. It shows how the old and new code generators produce different results for the `f(1)` function due to differing cleanup timings.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.1;
contract C {
    function f(uint8 a) public pure returns (uint r1, uint r2)
    {
        a = ~a;
        assembly {
            r1 := a
        }
        r2 = a;
    }
}
```

--------------------------------

### Unchecked Arithmetic in Solidity

Source: https://docs.soliditylang.org/en/v0.8.30/types

Demonstrates how to perform arithmetic operations in Solidity without overflow checks using the `unchecked { ... }` block. This can be more gas-efficient but requires careful handling to prevent unexpected behavior.

```Solidity
uint8 a = 255;
uint8 b = 1;

// This would revert by default due to overflow
// uint8 c = a + b;

// Using unchecked block to allow overflow
unchecked {
    uint8 c = a + b;
    // c will be 0 (255 + 1 wraps around)
}
```

--------------------------------

### Robot Contract with Diagonal Movement - Solidity

Source: https://docs.soliditylang.org/en/v0.8.30/smtchecker

Demonstrates a smart contract for a robot on a 2D grid with diagonal movement. It includes modifiers and functions to control movement and an invariant check ensuring the sum of coordinates remains even.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.0;

contract Robot {
    int x = 0;
    int y = 0;

    modifier wall {
        require(x > type(int128).min && x < type(int128).max);
        require(y > type(int128).min && y < type(int128).max);
        _;
    }

    function moveLeftUp() wall public {
        --x;
        ++y;
    }

    function moveLeftDown() wall public {
        --x;
        --y;
    }

    function moveRightUp() wall public {
        ++x;
        ++y;
    }

    function moveRightDown() wall public {
        ++x;
        --y;
    }

    function inv() public view {
        assert((x + y) % 2 == 0);
    }
}

```

--------------------------------

### Solidity: Internal Library Functions for Array Manipulation

Source: https://docs.soliditylang.org/en/v0.8.30/types

Illustrates the use of internal functions within a library for array manipulation. It includes functions for mapping elements using a provided function, reducing an array to a single value, and generating a range of numbers.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

library ArrayUtils {
    // internal functions can be used in internal library functions because
    // they will be part of the same code context
    function map(uint[] memory self, function (uint) pure returns (uint) f)
        internal
        pure
        returns (uint[] memory r)
    {
        r = new uint[](self.length);
        for (uint i = 0; i < self.length; i++) {
            r[i] = f(self[i]);
        }
    }

    function reduce(
        uint[] memory self,
        function (uint, uint) pure returns (uint) f
    )
        internal
        pure
        returns (uint r)
    {
        r = self[0];
        for (uint i = 1; i < self.length; i++) {
            r = f(r, self[i]);
        }
    }

    function range(uint length) internal pure returns (uint[] memory r) {
        r = new uint[](length);
        for (uint i = 0; i < r.length; i++) {
            r[i] = i;
        }
    }
}


contract Pyramid {
    using ArrayUtils for *;

    function pyramid(uint l) public pure returns (uint) {
        return ArrayUtils.range(l).map(square).reduce(sum);
    }

    function square(uint x) internal pure returns (uint) {
        return x * x;
    }

    function sum(uint x, uint y) internal pure returns (uint) {
        return x + y;
    }
}

```

--------------------------------

### Formal Specification of Yul Syntax

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Defines the grammatical structure of Yul code. This specification outlines the allowed components of Yul programs, including blocks, function definitions, variable declarations, assignments, conditional statements, loops, and literals.

```Yul Grammar
Block = '{' Statement* '}'
Statement =
    Block |
    FunctionDefinition |
    VariableDeclaration |
    Assignment |
    If |
    Expression |
    Switch |
    ForLoop |
    BreakContinue |
    Leave
FunctionDefinition =
    'function' Identifier '(' TypedIdentifierList? ')'
    ( '->' TypedIdentifierList )? Block
VariableDeclaration =
    'let' ' TypedIdentifierList ( ':=' Expression )?
Assignment =
    IdentifierList ':=' Expression
Expression =
    FunctionCall | Identifier | Literal
If =
    'if' Expression Block
Switch =
    'switch' Expression ( Case+ Default? | Default )
Case =
    'case' Literal Block
Default =
    'default' Block
ForLoop =
    'for' Block Expression Block Block
BreakContinue =
    'break' | 'continue'
Leave = 'leave'
FunctionCall =
    Identifier '(' ( Expression ( ',' Expression )* )? ')'
Identifier = [a-zA-Z_$] [a-zA-Z_$0-9.]*
IdentifierList = Identifier ( ',' Identifier)*
TypeName = Identifier
TypedIdentifierList = Identifier ( ':' TypeName )? ( ',' Identifier ( ':' TypeName )? )*
Literal =
    (NumberLiteral | StringLiteral | TrueLiteral | FalseLiteral) ( ':' TypeName )?
NumberLiteral = HexNumber | DecimalNumber
StringLiteral = '"' ([^"\r\n\\] | '\\' .)* '"'
TrueLiteral = 'true'
FalseLiteral = 'false'
HexNumber = '0x' [0-9a-fA-F]+
DecimalNumber = [0-9]+
```

--------------------------------

### EVM Dialect Arithmetic Opcodes

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Provides arithmetic operations compatible with the EVM. These include addition, subtraction, multiplication, division, modulo, and exponentiation. Some operations handle signed numbers and include modulo operations with arbitrary precision.

```solidity
add(x, y)
sub(x, y)
mul(x, y)
div(x, y)
sdiv(x, y)
mod(x, y)
smod(x, y)
exp(x, y)
addmod(x, y, m)
mulmod(x, y, m)
```

--------------------------------

### Eliminate Redundant Stores (Solidity)

Source: https://docs.soliditylang.org/en/v0.8.30/internals/optimizer

The UnusedStoreEliminator removes redundant sstore and memory store statements. For sstore, it removes a statement if all outgoing code paths revert or overwrite the stored value without a read in between. For memory stores, it removes them if they are never read. Best run in SSA form. Prerequisites: Disambiguator, ForLoopInitRewriter.

```Solidity
{
    let c := calldataload(0)
    sstore(c, 1)
    if c {
        sstore(c, 2)
    }
    sstore(c, 3)
}
```

```Solidity
{
    let c := calldataload(0)
    if c { }
    sstore(c, 3)
}
```

--------------------------------

### EVM Dialect Memory Operations

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Functions for interacting with the EVM's memory. 'mload' reads 32 bytes from memory, 'mstore' writes 32 bytes, and 'mstore8' writes a single byte. 'msize' returns the current memory size, and 'mcopy' copies data within memory.

```solidity
mload(p)
mstore(p, v)
mstore8(p, v)
msize()
mcopy(t, f, s)
```

--------------------------------

### Solidity Metadata Structure

Source: https://docs.soliditylang.org/en/v0.8.30/metadata

Defines the expected JSON structure for Solidity metadata, including compilation target, libraries, and source file information. This format is used by the compiler to store details about the compilation process.

```json
{
  "compiler": {
    "version": "0.8.30"
  },
  "settings": {
    "compilationTarget": {
      "myDirectory/myFile.sol": "MyContract"
    },
    "libraries": {
      "MyLib.sol:MyLib": "0x123123..."
    }
  },
  "sources": {
    "settable": {
      "content": "contract settable is owned { uint256 private x = 0; function set(uint256 _x) public { if (msg.sender == owner) x = _x; } }",
      "keccak256": "0x234..."
    },
    "myDirectory/myFile.sol": {
      "keccak256": "0x123...",
      "license": "MIT",
      "urls": [
        "bzz-raw://7d7a...",
        "dweb:/ipfs/QmN..."
      ]
    }
  },
  "version": 1
}
```

--------------------------------

### Solidity Contract Emitting the Deposit Event

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

A Solidity contract demonstrating the declaration and emission of a custom 'Deposit' event. The 'Deposit' event includes indexed parameters 'from' and 'id', and a non-indexed 'value'.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.21 <0.9.0;

contract ClientReceipt {
    event Deposit(
        address indexed from,
        bytes32 indexed id,
        uint value
    );

    function deposit(bytes32 id) public payable {
        // Events are emitted using `emit`, followed by
        // the name of the event and the arguments
        // (if any) in parentheses. Any such invocation
        // (even deeply nested) can be detected from
        // the JavaScript API by filtering for `Deposit`.
        emit Deposit(msg.sender, id, msg.value);
    }
}

```

--------------------------------

### Solidity: Function call options syntax

Source: https://docs.soliditylang.org/en/v0.8.30/080-breaking-changes

Function call options in Solidity 0.8.30 must be provided in a single set of curly braces. Multiple sets of options are now invalid.

```Solidity
c.f{gas: 10000}{value: 1}()
```

```Solidity
c.f{gas: 10000, value: 1}()
```

--------------------------------

### Solidity Function Modifier Execution with Placeholder

Source: https://docs.soliditylang.org/en/v0.8.30/ir-breaking-changes

Highlights the behavioral difference in Solidity function modifiers when the placeholder `_;` is evaluated multiple times. The new code generator treats modifiers more like functions, re-initializing parameters and return variables for each `_;` evaluation. This contrasts with the old generator where changes to parameters persisted across `_;` executions.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0;
contract C {
    function f(uint a) public pure mod() returns (uint r) {
        r = a++;
    }
    modifier mod() { _; _;
    }
}

```

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.1 <0.9.0;

contract C {
    bool active = true;
    modifier mod()
    {
        _;
        active = false;
        _;
    }
    function foo() external mod() returns (uint ret)
    {
        if (active)
            ret = 1; // Same as ``return 1``
    }
}

```

--------------------------------

### Solidity Address Code

Source: https://docs.soliditylang.org/en/v0.8.30/units-and-global-variables

Retrieves the bytecode of a contract at a given address. The returned bytes can be empty if the address has no code.

```Solidity
bytes memory code = someAddress.code;
```

--------------------------------

### Solidity: Concatenate Strings

Source: https://docs.soliditylang.org/en/v0.8.30/units-and-global-variables

Concatenates a variable number of string arguments into a single string array.

```Solidity
string.concat(...) returns (string memory)
```

--------------------------------

### Solidity: Require Functions

Source: https://docs.soliditylang.org/en/v0.8.30/units-and-global-variables

Reverts execution if the boolean condition is not met. Use for input or external component errors. An optional string message can be provided.

```Solidity
require(bool condition)
require(bool condition, string memory message)
```

--------------------------------

### Solidity Destructuring Assignment and Multiple Return Values

Source: https://docs.soliditylang.org/en/v0.8.30/control-structures

Demonstrates returning multiple values from a function using tuples and assigning them to variables. It shows how to skip elements during assignment and swap values. Prior to 0.5.0, assignments to tuples of smaller sizes were allowed, but this is now disallowed.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.5.0 <0.9.0;

contract C {
    uint index;

    function f() public pure returns (uint, bool, uint) {
        return (7, true, 2);
    }

    function g() public {
        // Variables declared with type and assigned from the returned tuple,
        // not all elements have to be specified (but the number must match).
        (uint x, , uint y) = f();
        // Common trick to swap values -- does not work for non-value storage types.
        (x, y) = (y, x);
        // Components can be left out (also for variable declarations).
        (index, , ) = f(); // Sets the index to 7
    }
}

```

--------------------------------

### Solidity g function with pre-incremented arguments

Source: https://docs.soliditylang.org/en/v0.8.30/ir-breaking-changes

Illustrates how the g function evaluates arguments with pre-increment operators, highlighting differences in return values between old and new code generators. The function relies on the add function.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.1;
contract C {
    function add(uint8 a, uint8 b) public pure returns (uint8) {
        return a + b;
    }
    function g(uint8 a, uint8 b) public pure returns (uint8) {
        return add(++a + ++b, a + b);
    }
}
```

--------------------------------

### Solidity Low-Level STATICCALL

Source: https://docs.soliditylang.org/en/v0.8.30/units-and-global-variables

Performs a low-level STATICCALL to an address with a given payload. It forwards all available gas and returns success status and return data. STATICCALL prevents state modifications.

```Solidity
 (bool success, bytes memory returnData) = someAddress.staticcall(payload); 
```

--------------------------------

### Define Interface for Pre-0.5.0 Solidity Contract

Source: https://docs.soliditylang.org/en/v0.8.30/050-breaking-changes

This snippet demonstrates how to define an interface for a Solidity contract deployed with a version prior to 0.5.0. This interface allows newer contracts (v0.5.0+) to interact with the older contract's functions. It specifies external visibility and omits 'constant' where 'view' might be applicable, due to changes in `staticcall` behavior.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.5.0 <0.9.0;
interface OldContract {
    function someOldFunction(uint8 a) external;
    function anotherOldFunction() external returns (bool);
}
```

--------------------------------

### Solidity delete Operator Usage

Source: https://docs.soliditylang.org/en/v0.8.30/types

Demonstrates the 'delete' operator in Solidity, showing its effect on different data types including integers, arrays, and mappings. It explains how 'delete' resets values to their initial state and its specific behavior with complex types and storage references.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

contract DeleteExample {
    uint data;
    uint[] dataArray;
    mapping(uint => uint) public dataMapping;

    function f() public {
        uint x = data;
        delete x; // sets x to 0, does not affect data
        delete data; // sets data to 0, does not affect x
        
        uint[] storage y = dataArray;
        delete dataArray; // sets dataArray.length to zero, y is affected
        assert(y.length == 0);

        dataMapping[1] = 100;
        delete dataMapping[1]; // deletes the key-value pair from the mapping
        assert(dataMapping[1] == 0);
    }

    function g() public {
      // Example showing 'delete' on a struct (if defined)
      // struct MyStruct { uint a; uint b; } 
      // MyStruct memory s = MyStruct(1, 2);
      // delete s; // s.a becomes 0, s.b becomes 0
    }
}
```

--------------------------------

### Solidity: Specify ABI coder version

Source: https://docs.soliditylang.org/en/v0.8.30/080-breaking-changes

Shows how to explicitly select the ABI coder version in Solidity. `pragma abicoder v2;` is the recommended way to use ABI coder v2, which is the default from version 0.8.0 onwards. `pragma experimental ABIEncoderV2;` is deprecated.

```Solidity
pragma solidity ^0.8.0;

// Use ABI coder v2 (default in 0.8.0+)
contract MyContractV2 {
    // ... implementation
}

// Explicitly use ABI coder v1 (older behavior)
pragma abicoder v1;
contract MyContractV1 {
    // ... implementation
}
```

--------------------------------

### Solidity Type Information

Source: https://docs.soliditylang.org/en/v0.8.30/cheatsheet

Enables introspection of contract types, interfaces, and integer types to retrieve metadata such as names, bytecode, interface IDs, and min/max values. This is useful for meta-programming and external interactions.

```Solidity
string contractName = type(MyContract).name;
uint maxValue = type(uint256).max;
```

--------------------------------

### Specify SMTChecker Verification Targets

Source: https://docs.soliditylang.org/en/v0.8.30/smtchecker

Customizes the types of verification targets the SMTChecker analyzes. Targets can be specified as a comma-separated list in the CLI or an array in JSON. All targets are checked by default, except for overflow and underflow checks in Solidity versions >= 0.8.7.

```bash
--model-checker-targets assert,overflow
```

```json
"settings.modelChecker.targets": ["assert", "overflow"]
```

--------------------------------

### Solidity Array Size Modification with push() and pop()

Source: https://docs.soliditylang.org/en/v0.8.30/types

Demonstrates how to change the length of dynamic arrays in Solidity using the push() and pop() functions. push() appends a new zero-initialized element, while pop() removes and deletes the last element. The gas cost for pop() depends on the size of the removed element.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

contract ArrayContract {
    bool[2][] pairsOfFlags;

    function changeFlagArraySize(uint newSize) public {
        // using push and pop is the only way to change the
        // length of an array
        if (newSize < pairsOfFlags.length) {
            while (pairsOfFlags.length > newSize)
                pairsOfFlags.pop();
        } else if (newSize > pairsOfFlags.length) {
            while (pairsOfFlags.length < newSize)
                pairsOfFlags.push();
        }
    }

    function addFlag(bool[2] memory flag) public returns (uint) {
        pairsOfFlags.push(flag);
        return pairsOfFlags.length;
    }
}

```

--------------------------------

### Solidity: SHA256 Hash

Source: https://docs.soliditylang.org/en/v0.8.30/units-and-global-variables

Computes the SHA-256 hash of the input bytes.

```Solidity
sha256(bytes memory) returns (bytes32)
```

--------------------------------

### Solidity Contract-related Keywords

Source: https://docs.soliditylang.org/en/v0.8.30/cheatsheet

Keywords like `this`, `super`, and `selfdestruct` provide access to the current contract instance, parent contract, and control over contract lifecycle and fund transfer. `selfdestruct` is used to destroy a contract and send its balance.

```Solidity
address payable recipient = payable(0x123);
selfdestruct(recipient);
```

--------------------------------

### Solidity Library for Array Search

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

This Solidity code defines a library named 'Search' that extends the uint array type. It includes a function 'indexOf' to find the index of a specific uint value within an array. The library is then used by a contract 'C' to manage and modify an array of uints.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.13;

library Search {
    function indexOf(uint[] storage self, uint value)
        public
        view
        returns (uint)
    {
        for (uint i = 0; i < self.length; i++)
            if (self[i] == value) return i;
        return type(uint).max;
    }
}
using Search for uint[];

contract C {
    uint[] data;

    function append(uint value) public {
        data.push(value);
    }

    function replace(uint from, uint to) public {
        // This performs the library function call
        uint index = data.indexOf(from);
        if (index == type(uint).max)
            data.push(to);
        else
            data[index] = to;
    }
}
```

--------------------------------

### Solidity Internal vs. External Getter Access

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Illustrates the difference between internal and external access to a public state variable in Solidity. Internal access directly references the state variable, while external access calls the auto-generated getter function.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

contract C {
    uint public data;
    function x() public returns (uint) {
        data = 3; // internal access
        return this.data(); // external access
    }
}
```

--------------------------------

### Solidity Interface Definition

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Defines a Solidity interface 'Token' with an enum 'TokenType', a struct 'Coin', and a function signature 'transfer'. Interfaces have restrictions like no implemented functions or state variables.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.2 <0.9.0;

interface Token {
    enum TokenType { Fungible, NonFungible }
    struct Coin { string obverse; string reverse; }
    function transfer(address recipient, uint amount) external;
}
```

--------------------------------

### Solidity: Handling Integer Overflows with 'unchecked'

Source: https://docs.soliditylang.org/en/v0.8.30/security-considerations

Illustrates how Solidity's integer types can overflow and how the 'unchecked' block can be used to allow wrapping behavior instead of reverting. This is crucial for managing arithmetic operations safely.

```Solidity
uint8 x = 255;
uint8 y = 1;
return x + y;

```

```Solidity
uint8 x = 255;
uint8 y = 1;
// This code would return 0 if wrapped in unchecked {
return x + y;
}

```

--------------------------------

### Assigning Function Pointer Address and Selector in Solidity

Source: https://docs.soliditylang.org/en/v0.8.30/assembly

Demonstrates how to assign a new address and function selector to an external function pointer within inline assembly. Requires Solidity 0.8.10 or higher.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.10 <0.9.0;

contract C {
    // Assigns a new selector and address to the return variable @fun
    function combineToFunctionPointer(address newAddress, uint newSelector) public pure returns (function() external fun) {
        assembly {
            fun.selector := newSelector
            fun.address  := newAddress
        }
    }
}
```

--------------------------------

### Encoding of Solidity Function Call with Dynamic Types

Source: https://docs.soliditylang.org/en/v0.8.30/abi-spec

Demonstrates the ABI encoding for a Solidity function call with a mix of static and dynamic types: uint256, uint32[], bytes10, and bytes. It shows how each argument is represented, including offsets for dynamic types.

```text
0x8be65246
  0000000000000000000000000000000000000000000000000000000000000123
  0000000000000000000000000000000000000000000000000000000000000080
  3132333435363738393000000000000000000000000000000000000000000000
  00000000000000000000000000000000000000000000000000000000000000e0
  0000000000000000000000000000000000000000000000000000000000000002
  0000000000000000000000000000000000000000000000000000000000000456
  0000000000000000000000000000000000000000000000000000000000000789
  000000000000000000000000000000000000000000000000000000000000000d
  48656c6c6f2c20776f726c642100000000000000000000000000000000000000
```

--------------------------------

### Solidity: Token Transfer Property Verification with Interface

Source: https://docs.soliditylang.org/en/v0.8.30/smtchecker

Shows a correct implementation in Solidity for verifying the `transfer` function of a token contract using an interface. The `Test` contract interacts with `TokenCorrect` through the `Token` interface, ensuring that the transfer operation correctly updates balances.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.0;

interface Token {
    function balanceOf(address _a) external view returns (uint);
    function transfer(address _to, uint _amt) external;
}

contract TokenCorrect is Token {
    mapping (address => uint) balance;
    constructor(address _a, uint _b) {
        balance[_a] = _b;
    }
    function balanceOf(address _a) public view override returns (uint) {
        return balance[_a];
    }
    function transfer(address _to, uint _amt) public override {
        require(balance[msg.sender] >= _amt);
        balance[msg.sender] -= _amt;
        balance[_to] += _amt;
    }
}

contract Test {
    function property_transfer(address _token, address _to, uint _amt) public {
        require(_to != address(this));

        TokenCorrect t = TokenCorrect(_token);

        uint xPre = t.balanceOf(address(this));
        require(xPre >= _amt);
        uint yPre = t.balanceOf(_to);

        t.transfer(_to, _amt);
        uint xPost = t.balanceOf(address(this));
        uint yPost = t.balanceOf(_to);

        assert(xPost == xPre - _amt);
        assert(yPost == yPre + _amt);
    }
}

```

--------------------------------

### Solidity Contract Metadata JSON Structure

Source: https://docs.soliditylang.org/en/v0.8.30/metadata

This JSON structure represents the metadata generated by the Solidity compiler. It includes compiler details, language, and output information such as ABI and developer/user documentation (NatSpec).

```JSON
{
  "compiler": {
    "keccak256": "0x123...",
    "version": "0.8.2+commit.661d1103"
  },
  "language": "Solidity",
  "output": {
    "abi": [/* ... */],
    "devdoc": {
      "author": "John Doe",
      "details": "Interface of the ERC20 standard as defined in the EIP. See https://eips.ethereum.org/EIPS/eip-20 for details",
      "errors": {
        "MintToZeroAddress()" : {
          "details": "Cannot mint to zero address"
        }
      },
      "events": {
        "Transfer(address,address,uint256)": {
          "details": "Emitted when `value` tokens are moved from one account (`from`) toanother (`to`).",
          "params": {
            "from": "The sender address",
            "to": "The receiver address",
            "value": "The token amount"
          }
        }
      },
      "kind": "dev",
      "methods": {
        "transfer(address,uint256)": {
          "details": "Returns a boolean value indicating whether the operation succeeded. Must be called by the token holder address",
          "params": {
            "_value": "The amount tokens to be transferred",
            "_to": "The receiver address"
          },
          "returns": {
            "success": "a boolean value indicating whether the operation succeeded"
          }
        }
      },
      "stateVariables": {
        "owner": {
          "details": "Must be set during contract creation. Can then only be changed by the owner"
        }
      },
      "title": "MyERC20: an example ERC20",
      "version": 1
    },
    "userdoc": {
      "errors": {
        "ApprovalCallerNotOwnerNorApproved()": [
          {
            "notice": "The caller must own the token or be an approved operator."
          }
        ]
      },
      "events": {
        "Transfer(address,address,uint256)": {
          "notice": "`_value` tokens have been moved from `from` to `to`"
        }
      },
      "kind": "user",
      "methods": {
        "transfer(address,uint256)": {
          "notice": "Transfers `_value` tokens to address `_to`"
        }
      }
    }
  }
}
```

--------------------------------

### Solidity User-defined Value Type and Fixed-Point Library

Source: https://docs.soliditylang.org/en/v0.8.30/types

Defines a user-defined value type `UFixed256x18` for representing fixed-point numbers and a library `FixedMath` to perform arithmetic operations on this type. Includes functions for addition, multiplication, flooring, and conversion from uint256.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.8;

// Represent a 18 decimal, 256 bit wide fixed point type using a user-defined value type.
type UFixed256x18 is uint256;

/// A minimal library to do fixed point operations on UFixed256x18.
library FixedMath {
    uint constant multiplier = 10**18;

    /// Adds two UFixed256x18 numbers. Reverts on overflow, relying on checked
    /// arithmetic on uint256.
    function add(UFixed256x18 a, UFixed256x18 b) internal pure returns (UFixed256x18) {
        return UFixed256x18.wrap(UFixed256x18.unwrap(a) + UFixed256x18.unwrap(b));
    }
    /// Multiplies UFixed256x18 and uint256. Reverts on overflow, relying on checked
    /// arithmetic on uint256.
    function mul(UFixed256x18 a, uint256 b) internal pure returns (UFixed256x18) {
        return UFixed256x18.wrap(UFixed256x18.unwrap(a) * b);
    }
    /// Take the floor of a UFixed256x18 number.
    /// @return the largest integer that does not exceed `a`.
    function floor(UFixed256x18 a) internal pure returns (uint256) {
        return UFixed256x18.unwrap(a) / multiplier;
    }
    /// Turns a uint256 into a UFixed256x18 of the same value.
    /// Reverts if the integer is too large.
    function toUFixed256x18(uint256 a) internal pure returns (UFixed256x18) {
        return UFixed256x18.wrap(a * multiplier);
    }
}

```

--------------------------------

### Solidity: Pad Higher-Order Bits on Integer Conversion

Source: https://docs.soliditylang.org/en/v0.8.30/types

Shows explicit conversion of a smaller integer type to a larger one, where the higher-order bits are padded with zeros. The value remains the same, ensuring equality assertion.

```solidity
uint16 a = 0x1234;
uint32 b = uint32(a); // b will be 0x00001234 now
assert(a == b);

```

--------------------------------

### Solidity Code Update: Inline Assembly Opcodes

Source: https://docs.soliditylang.org/en/v0.8.30/060-breaking-changes

Shows the required syntax update for inline assembly opcodes in Solidity that do not accept arguments. Parentheses `()` must now be appended.

```solidity
// Old syntax
// pc
// gas

// New syntax
pc();
gas();
```

--------------------------------

### Boolean Operators in Solidity

Source: https://docs.soliditylang.org/en/v0.8.30/types

Demonstrates the logical and equality operators available for boolean types in Solidity. The '&&' and '||' operators support short-circuiting, meaning the second operand is only evaluated if necessary.

```Solidity
// Logical NOT
!boolVariable;

// Logical AND
boolVariable1 && boolVariable2;

// Logical OR
boolVariable1 || boolVariable2;

// Equality
boolVariable1 == boolVariable2;

// Inequality
boolVariable1 != boolVariable2;
```

--------------------------------

### Solidity Address Balance

Source: https://docs.soliditylang.org/en/v0.8.30/units-and-global-variables

Accesses the Ether balance of an address in Wei. This is a read-only property.

```Solidity
uint256 balance = payable(someAddress).balance;
```

--------------------------------

### Solidity State Machine with Stage and Time Transitions

Source: https://docs.soliditylang.org/en/v0.8.30/common-patterns

This Solidity contract implements a state machine using custom modifiers 'atStage' and 'timedTransitions'. 'atStage' ensures a function is callable only in a specific stage, while 'timedTransitions' handles automatic transitions based on time elapsed since contract creation. It also includes a 'transitionNext' modifier for manual progression to the next stage after function execution.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.4;

contract StateMachine {
    enum Stages {
        AcceptingBlindedBids,
        RevealBids,
        AnotherStage,
        AreWeDoneYet,
        Finished
    }
    /// Function cannot be called at this time.
    error FunctionInvalidAtThisStage();

    // This is the current stage.
    Stages public stage = Stages.AcceptingBlindedBids;

    uint public creationTime = block.timestamp;

    modifier atStage(Stages stage_) {
        if (stage != stage_)
            revert FunctionInvalidAtThisStage();
        _;
    }

    function nextStage() internal {
        stage = Stages(uint(stage) + 1);
    }

    // Perform timed transitions. Be sure to mention
    // this modifier first, otherwise the guards
    // will not take the new stage into account.
    modifier timedTransitions() {
        if (stage == Stages.AcceptingBlindedBids &&
                    block.timestamp >= creationTime + 10 days)
            nextStage();
        if (stage == Stages.RevealBids &&
                block.timestamp >= creationTime + 12 days)
            nextStage();
        // The other stages transition by transaction
        _;
    }

    // Order of the modifiers matters here!
    function bid(
    )
        public
        payable
        timedTransitions
        atStage(Stages.AcceptingBlindedBids)
    {
        // We will not implement that here
    }

    function reveal(
    )
        public
        timedTransitions
        atStage(Stages.RevealBids)
    {
    }

    // This modifier goes to the next stage
    // after the function is done.
    modifier transitionNext(
    )
    {
        _;
        nextStage();
    }

    function g(
    )
        public
        timedTransitions
        atStage(Stages.AnotherStage)
        transitionNext
    {
    }

    function h(
    )
        public
        timedTransitions
        atStage(Stages.AreWeDoneYet)
        transitionNext
    {
    }

    function i(
    )
        public
        timedTransitions
        atStage(Stages.Finished)
    {
    }
}

```

--------------------------------

### Solidity: Concatenate Bytes

Source: https://docs.soliditylang.org/en/v0.8.30/units-and-global-variables

Concatenates a variable number of bytes and bytes1 to bytes32 arguments into a single byte array.

```Solidity
bytes.concat(...) returns (bytes memory)
```

--------------------------------

### Solidity Contract Code Execution (callcode)

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Similar to `call`, but executes the code from the target address within the context of the current contract. This means `msg.sender` and `msg.value` remain unchanged. Returns 1 on success and 0 on error.

```Solidity
bool success = callcode(gas, target_address, value, data_ptr, data_size, output_ptr, output_size);
```

--------------------------------

### Solidity: Explicit Conversion to Address Payable

Source: https://docs.soliditylang.org/en/v0.8.30/types

Demonstrates the explicit conversion from a contract type to an address payable type using the `payable()` constructor. This conversion is only allowed if the contract can receive Ether, meaning it has a receive or a payable fallback function. An exception is `payable(0)`.

```solidity
pragma solidity ^0.8.0;

contract ExampleContract {
    function getPayableAddress(address payable _addr) public pure returns (address payable) {
        return _addr;
    }

    function getAddressFromPayable(address payable _addr) public pure returns (address) {
        return _addr;
    }

    // Explicit conversion from address to address payable
    function explicitConvert(address _addr) public pure returns (address payable) {
        return payable(_addr);
    }

    // Example of payable(0)
    function zeroAddress() public pure returns (address payable) {
        return payable(0);
    }
}
```

--------------------------------

### Solidity Function Type Conversion Rules

Source: https://docs.soliditylang.org/en/v0.8.30/types

Describes the rules for implicit conversion between Solidity function types, focusing on state mutability. Pure functions can convert to view and non-payable; view functions to non-payable; and payable functions to non-payable. It explains the reasoning behind these restrictions.

```Solidity
// pure functions can be converted to view and non-payable functions
// view functions can be converted to non-payable functions
// payable functions can be converted to non-payable functions

// Example of a payable function being converted to non-payable:
function payableFunc() public payable {
    // ...
}

function nonPayableFunc() public pure {
    // ...
}

// This assignment is valid:
nonPayableFunc = payableFunc;
```

--------------------------------

### Yul Data Copy (datacopy)

Source: https://docs.soliditylang.org/en/v0.8.30/yul

The Yul equivalent of the `codecopy` opcode. It copies data from the code section of the contract to a specified memory location. Takes a target memory location, source offset, and length.

```Yul
datacopy(target_memory_offset, source_code_offset, length);
```

--------------------------------

### Solidity: Handle .call() family return values

Source: https://docs.soliditylang.org/en/v0.8.30/050-breaking-changes

In Solidity v0.5.0, the .call(), .delegatecall(), and .staticcall() functions now return a tuple of (bool success, bytes memory data). This allows access to the return data, unlike previous versions where only a boolean success flag was returned.

```Solidity
// Before v0.5.0
bool success = otherContract.call("f");

// After v0.5.0
(bool success, bytes memory data) = otherContract.call("f");
```

--------------------------------

### Solidity: Use require for input validation and assert for internal checks

Source: https://docs.soliditylang.org/en/v0.8.30/control-structures

Demonstrates using `require` to validate the transaction value and `assert` to check the contract's internal state after a transfer. `require` checks external conditions, while `assert` verifies internal invariants.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.5.0 <0.9.0;

contract Sharer {
    function sendHalf(address payable addr) public payable returns (uint balance) {
        require(msg.value % 2 == 0, "Even value required.");
        uint balanceBeforeTransfer = address(this).balance;
        addr.transfer(msg.value / 2);
        // Since transfer throws an exception on failure and
        // cannot call back here, there should be no way for us to
        // still have half of the Ether.
        assert(address(this).balance == balanceBeforeTransfer - msg.value / 2);
        return address(this).balance;
    }
}
```

--------------------------------

### Solidity: Literal Conversion to Fixed-Size Byte Arrays

Source: https://docs.soliditylang.org/en/v0.8.30/types

Explains rules for converting literals to fixed-size byte arrays. Hexadecimal literals must match the size exactly, while zero literals can convert to any size. String literals convert if their length fits.

```solidity
bytes2 a = 54321; // not allowed
bytes2 b = 0x12; // not allowed
bytes2 c = 0x123; // not allowed
bytes2 d = 0x1234; // fine
bytes2 e = 0x0012; // fine
bytes4 f = 0; // fine
bytes4 g = 0x0; // fine

bytes2 a = hex"1234"; // fine
bytes2 b = "xy"; // fine
bytes2 c = hex"12"; // fine
bytes2 e = "x"; // fine
bytes2 f = "xyz"; // not allowed

```

--------------------------------

### Solidity: Adjust gas and value with call modifier

Source: https://docs.soliditylang.org/en/v0.8.30/types

Illustrates how to specify the gas amount and Ether value sent with a 'call'. The 'gas' modifier allows setting a gas limit, and the 'value' modifier sends a specified amount of Ether. These modifiers can be combined, and their order does not affect execution.

```Solidity
address(nameReg).call{gas: 1000000}(abi.encodeWithSignature("register(string)", "MyName"));
```

```Solidity
address(nameReg).call{value: 1 ether}(abi.encodeWithSignature("register(string)", "MyName"));
```

```Solidity
address(nameReg).call{gas: 1000000, value: 1 ether}(abi.encodeWithSignature("register(string)", "MyName"));
```

--------------------------------

### Solidity ABI Coder Pragmas

Source: https://docs.soliditylang.org/en/v0.8.30/080-breaking-changes

Shows how to specify the ABI coder version in Solidity. `pragma abicoder v1;` maintains the old ABI encoding, while `pragma experimental ABIEncoderV2` or `pragma abicoder v2` are now redundant.

```Solidity
pragma abicoder v1;
```

```Solidity
pragma abicoder v2;
```

--------------------------------

### Yul AST Evaluation Function E

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Defines the evaluation function E for Yul's AST, overloaded for different node types. E takes global and local state objects and an AST node, returning updated states and evaluation results. It handles statements, expressions, and control flow constructs like break, continue, and leave.

```Yul
E(G, L, <{St1, ..., Stn}>: Block) =
    let G1, L1, mode = E(G, L, St1, ..., Stn)
    let L2 be a restriction of L1 to the identifiers of L
    G1, L2, mode
E(G, L, St1, ..., Stn: Statement) =
    if n is zero:
        G, L, regular
    else:
        let G1, L1, mode = E(G, L, St1)
        if mode is regular then
            E(G1, L1, St2, ..., Stn)
        otherwise
            G1, L1, mode
E(G, L, FunctionDefinition) =
    G, L, regular
E(G, L, <let var_1, ..., var_n := rhs>: VariableDeclaration) =
    E(G, L, <var_1, ..., var_n := rhs>: Assignment)
E(G, L, <let var_1, ..., var_n>: VariableDeclaration) =
    let L1 be a copy of L where L1[$var_i] = 0 for i = 1, ..., n
    G, L1, regular
E(G, L, <var_1, ..., var_n := rhs>: Assignment) =
    let G1, L1, v1, ..., vn = E(G, L, rhs)
    let L2 be a copy of L1 where L2[$var_i] = vi for i = 1, ..., n
    G1, L2, regular
E(G, L, <for { i1, ..., in } condition post body>: ForLoop) =
    if n >= 1:
        let G1, L1, mode = E(G, L, i1, ..., in)
        // mode has to be regular or leave due to the syntactic restrictions
        if mode is leave then
            G1, L1 restricted to variables of L, leave
        otherwise
            let G2, L2, mode = E(G1, L1, for {} condition post body)
            G2, L2 restricted to variables of L, mode
    else:
        let G1, L1, v = E(G, L, condition)
        if v is false:
            G1, L1, regular
        else:
            let G2, L2, mode = E(G1, L, body)
            if mode is break:
                G2, L2, regular
            otherwise if mode is leave:
                G2, L2, leave
            else:
                G3, L3, mode = E(G2, L2, post)
                if mode is leave:
                    G3, L3, leave
                otherwise
                    E(G3, L3, for {} condition post body)
E(G, L, break: BreakContinue) =
    G, L, break
E(G, L, continue: BreakContinue) =
    G, L, continue
E(G, L, leave: Leave) =
    G, L, leave
E(G, L, <if condition body>: If) =
    let G0, L0, v = E(G, L, condition)
    if v is true:
        E(G0, L0, body)
    else:
        G0, L0, regular
E(G, L, <switch condition case l1:t1 st1 ... case ln:tn stn>: Switch) =
    E(G, L, switch condition case l1:t1 st1 ... case ln:tn stn default {})
E(G, L, <switch condition case l1:t1 st1 ... case ln:tn stn default st'>: Switch) =
    let G0, L0, v = E(G, L, condition)
    // i = 1 .. n
    // Evaluate literals, context doesn't matter
    let _, _, v1 = E(G0, L0, l1)
    ...
    let _, _, vn = E(G0, L0, ln)
    if there exists smallest i such that vi = v:
        E(G0, L0, sti)
    else:
        E(G0, L0, st')

E(G, L, <name>: Identifier) =
    G, L, L[$name]
E(G, L, <fname(arg1, ..., argn)>: FunctionCall) =
    G1, L1, vn = E(G, L, argn)
    ...
    G(n-1), L(n-1), v2 = E(G(n-2), L(n-2), arg2)
    Gn, Ln, v1 = E(G(n-1), L(n-1), arg1)
    Let <function fname (param1, ..., paramn) -> ret1, ..., retm block>
    be the function of name $fname visible at the point of the call.
    Let L' be a new local state such that
    L'[$parami] = vi and L'[$reti] = 0 for all i.
    Let G'', L'', mode = E(Gn, L', block)
    G'', Ln, L''[$ret1], ..., L''[$retm]
E(G, L, l: StringLiteral) = G, L, str(l),
    where str is the string evaluation function,
    which for the EVM dialect is defined in the section 'Literals' above
E(G, L, n: HexNumber) = G, L, hex(n)
    where hex is the hexadecimal evaluation function,
    which turns a sequence of hexadecimal digits into their big endian value
E(G, L, n: DecimalNumber) = G, L, dec(n),
    where dec is the decimal evaluation function,
    which turns a sequence of decimal digits into their big endian value
```

--------------------------------

### Remove Unused Function Parameters (Solidity)

Source: https://docs.soliditylang.org/en/v0.8.30/internals/optimizer

This optimizer step removes unused parameters from functions. It replaces the original function with a new 'linking' function that omits the unused parameters and redirects calls. Dependencies include Disambiguator, FunctionHoister, and LiteralRematerialiser (optional).

```Solidity
function f(a,b) -> x { x := div(a,b) }
function f2(a,b,c) -> x, y { x := f(a,b) }
```

--------------------------------

### Full ABI Encoding of a Function with Dynamic Arrays (Solidity)

Source: https://docs.soliditylang.org/en/v0.8.30/abi-spec

Illustrates the complete ABI encoding for a Solidity function that accepts two dynamic arrays: one of uint256s and one of strings. This includes the function selector, offsets to the dynamic arrays, counts of elements within each array, and the encoded data for each element, including nested arrays and strings.

```text
0x2289b18c                                                            - function signature
 0 - f                                                                - offset of [[1, 2], [3]]
 1 - g                                                                - offset of ["one", "two", "three"]
 2 - 0000000000000000000000000000000000000000000000000000000000000002 - count for [[1, 2], [3]]
 3 - 0000000000000000000000000000000000000000000000000000000000000040 - offset of [1, 2]
 4 - 00000000000000000000000000000000000000000000000000000000000000a0 - offset of [3]
 5 - 0000000000000000000000000000000000000000000000000000000000000002 - count for [1, 2]
 6 - 0000000000000000000000000000000000000000000000000000000000000001 - encoding of 1
 7 - 0000000000000000000000000000000000000000000000000000000000000002 - encoding of 2
 8 - 0000000000000000000000000000000000000000000000000000000000000001 - count for [3]
 9 - 0000000000000000000000000000000000000000000000000000000000000003 - encoding of 3
10 - 0000000000000000000000000000000000000000000000000000000000000003 - count for ["one", "two", "three"]
11 - 0000000000000000000000000000000000000000000000000000000000000060 - offset for "one"
12 - 00000000000000000000000000000000000000000000000000000000000000a0 - offset for "two"
13 - 00000000000000000000000000000000000000000000000000000000000000e0 - offset for "three"
14 - 0000000000000000000000000000000000000000000000000000000000000003 - count for "one"
15 - 6f6e650000000000000000000000000000000000000000000000000000000000 - encoding of "one"
16 - 0000000000000000000000000000000000000000000000000000000000000003 - count for "two"
17 - 74776f0000000000000000000000000000000000000000000000000000000000 - encoding of "two"
```

--------------------------------

### Solidity Getter for Public State Variable

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Demonstrates how the Solidity compiler automatically generates a getter function for a public state variable 'data'. This function can be called externally to retrieve the variable's value.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract C {
    uint public data = 42;
}

contract Caller {
    C c = new C();
    function f() public view returns (uint) {
        return c.data();
    }
}
```

--------------------------------

### Solidity: Assert Function

Source: https://docs.soliditylang.org/en/v0.8.30/units-and-global-variables

Causes a Panic error and state reversion if the boolean condition is not met. Use for internal errors.

```Solidity
assert(bool condition)
```

--------------------------------

### Set SMTChecker Timeout

Source: https://docs.soliditylang.org/en/v0.8.30/smtchecker

Configures the timeout for SMTChecker queries. A value of 0 disables the timeout. This can be set via the command line or JSON configuration.

```bash
--model-checker-timeout <time>
```

```json
"settings.modelChecker.timeout": <time>
```

--------------------------------

### Solidity Static Contract Call (staticcall)

Source: https://docs.soliditylang.org/en/v0.8.30/yul

A read-only version of `call`. It executes the code from the target address but disallows any state modifications. Returns 1 on success and 0 on error.

```Solidity
bool success = staticcall(gas, target_address, data_ptr, data_size, output_ptr, output_size);
// Example usage:
// (bool success, bytes memory returndata) = target_contract.staticcall(abi.encodeWithSignature("functionName(uint256)", arg1));
```

--------------------------------

### Solidity: Error data for revert("string")

Source: https://docs.soliditylang.org/en/v0.8.30/control-structures

Shows the abi-encoded error data returned when using `revert("description")`. This data includes the function selector for `Error(string)`, data offset, string length, and the string content itself.

```hex
0x08c379a0                                                         // Function selector for Error(string)
0x0000000000000000000000000000000000000000000000000000000000000020 // Data offset
0x000000000000000000000000000000000000000000000000000000000000001a // String length
0x4e6f7420656e6f7567682045746865722070726f76696465642e000000000000 // String data
```

--------------------------------

### Solidity: Override Function with Multiple Inheritance

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Illustrates overriding a function inherited from multiple base contracts. When a function is defined in multiple unrelated bases, it must be explicitly overridden, specifying all bases that define the same function and haven't been overridden yet.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

contract Base1
{
    function foo() virtual public {}
}

contract Base2
{
    function foo() virtual public {}
}

contract Inherited is Base1, Base2
{
    // Derives from multiple bases defining foo(), so we must explicitly
    // override it
    function foo() public override(Base1, Base2) {}
}

```

--------------------------------

### Solidity Type to ABI Type Mapping

Source: https://docs.soliditylang.org/en/v0.8.30/abi-spec

Illustrates how certain Solidity types are represented in the Contract ABI. This mapping is crucial for understanding data encoding and interoperability.

```plaintext
Solidity | ABI
address payable | address
contract | address
enum | uint8
user defined value types | its underlying value type
struct | tuple
```

--------------------------------

### Solidity Monotonic Function Assertion

Source: https://docs.soliditylang.org/en/v0.8.30/smtchecker

This Solidity contract demonstrates the use of 'assert' to verify a monotonic property. The 'inv' function ensures that for any two inputs 'a' and 'b' where 'b' is greater than 'a', the output of 'f(b)' is also greater than 'f(a)'.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.0;

contract Monotonic {
    function f(uint x) internal pure returns (uint) {
        require(x < type(uint128).max);
        return x * 42;
    }

    function inv(uint a, uint b) public pure {
        require(b > a);
        assert(f(b) > f(a));
    }
}

```

--------------------------------

### ABI Encoding for sam(bytes,bool,uint256[])

Source: https://docs.soliditylang.org/en/v0.8.30/abi-spec

Shows the ABI encoding for calling the 'sam' function with a dynamic byte array, a boolean, and a dynamic uint array. It details the encoding of dynamic types, including their lengths and data offsets.

```hex
0xa5643bf20000000000000000000000000000000000000000000000000000000000000060000000000000000000000000000000000000000000000000000000000000001000000000000000000000000000000000000000000000000000000000000000a000000000000000000000000000000000000000000000000000000000000000464617665000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000003000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000003
```

--------------------------------

### Show Unproved Targets in SMTChecker

Source: https://docs.soliditylang.org/en/v0.8.30/smtchecker

Enables the display of specific unproved verification targets. If there are any unproved targets, the SMTChecker issues a warning indicating their count. This option can be toggled via the CLI or JSON configuration.

```bash
--model-checker-show-unproved
```

```json
"settings.modelChecker.showUnproved": true
```

--------------------------------

### Solidity Multiple Inheritance Event Emission (without super)

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

This Solidity code snippet illustrates a scenario where multiple inheritance is used, but the `super` keyword is not employed. This can lead to unexpected behavior where some base contract functions are bypassed, resulting in an incorrect event emission sequence.

```solidity
contract Emittable {
    event Emitted();
    function emitEvent() virtual public {
        emit Emitted();
    }
}

contract Base1 is Emittable {
    event Base1Emitted();
    function emitEvent() public virtual override {
        /* Here, we emit an event to simulate some Base1 logic */
        emit Base1Emitted();
        Emittable.emitEvent();
    }
}

contract Base2 is Emittable {
    event Base2Emitted();
    function emitEvent() public virtual override {
        /* Here, we emit an event to simulate some Base2 logic */
        emit Base2Emitted();
        Emittable.emitEvent();
    }
}

contract Final is Base1, Base2 {
    event FinalEmitted();
    function emitEvent() public override(Base1, Base2) {
        /* Here, we emit an event to simulate some Final logic */
        emit FinalEmitted();
        Base2.emitEvent();
    }
}
```

--------------------------------

### Solidity: New External Call Syntax for Ether and Gas

Source: https://docs.soliditylang.org/en/v0.8.30/070-breaking-changes

Introduces the new syntax for specifying Ether and gas in external function and contract creation calls. The old syntax is now an error. This change aims for clearer and more concise expression of call options.

```Solidity
x.f{gas: 10000, value: 2 ether}(arg1, arg2)
```

--------------------------------

### Solidity: Implicit Conversion of Integer Literals

Source: https://docs.soliditylang.org/en/v0.8.30/types

Demonstrates how decimal and hexadecimal number literals can be implicitly converted to integer types if the target type is large enough to hold the value without truncation.

```solidity
uint8 a = 12; // fine
uint32 b = 1234; // fine
uint16 c = 0x123456; // fails, since it would have to truncate to 0x3456

```

--------------------------------

### Solidity Inheritance State Variable Initialization Order

Source: https://docs.soliditylang.org/en/v0.8.30/ir-breaking-changes

Demonstrates the change in state variable initialization order in Solidity contracts with inheritance. Previously, state variables were initialized after constructors ran. The new order initializes state variables for each contract in the hierarchy before running its constructor, affecting values derived from constructor calls.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.1;

contract A {
    uint x;
    constructor() {
        x = 42;
    }
    function f() public view returns(uint256) {
        return x;
    }
}
contract B is A {
    uint public y = f();
}

```

--------------------------------

### Solidity Compiler Known Bugs JSON Format

Source: https://docs.soliditylang.org/en/v0.8.30/bugs

This JSON structure represents a known bug in the Solidity compiler. It includes a unique identifier, name, summary, detailed description, optional links, version information (introduced and fixed), publish date, severity, triggering conditions, and checks for bug presence.

```json
[{
    "uid": "SOL-2023-3",
    "name": "VerbatimInvalidDeduplication",
    "summary": "All \"verbatim\" blocks are considered identical by deduplicator and can incorrectly be unified when surrounded by identical opcodes.",
    "description": "The block deduplicator is a step of the opcode-based optimizer which identifies equivalent assembly blocks and merges them into a single one. However, when blocks contained \"verbatim\", their comparison was performed incorrectly, leading to the collapse of assembly blocks which are identical except for the contents of the \"verbatim\" items. Since \"verbatim\" is only available in Yul, compilation of Solidity sources is not affected.",
    "link": "https://blog.soliditylang.org/2023/11/08/verbatim-invalid-deduplication-bug/",
    "introduced": "0.8.5",
    "fixed": "0.8.23",
    "severity": "low"
},
{
    "uid": "SOL-2023-2",
    "name": "FullInlinerNonExpressionSplitArgumentEvaluationOrder",
    "summary": "Optimizer sequences containing FullInliner do not preserve the evaluation order of arguments of inlined function calls in code that is not in expression-split form.",
    "description": "The bug is not present in expression-split code, because the evaluation order is fixed in that case. The bug is not present in non-optimized code.",
    "introduced": "0.8.0",
    "fixed": "0.8.23",
    "severity": "medium"
}]
```

--------------------------------

### Solidity Block and Transaction Properties

Source: https://docs.soliditylang.org/en/v0.8.30/cheatsheet

Accesses information about the current block and transaction context, including gas, sender, value, and chain details. These properties are fundamental for conditional logic and state management within smart contracts.

```Solidity
uint blockNum = block.number;
address sender = msg.sender;
uint value = msg.value;
```

--------------------------------

### External Function Members in Solidity

Source: https://docs.soliditylang.org/en/v0.8.30/types

Details the members available for external or public function types in Solidity. Specifically, `.address` returns the contract address and `.selector` returns the ABI function selector. Mentions deprecated members `.gas()` and `.value()`.

```Solidity
contract MyContract {
    function doSomething() public pure returns (bool) {
        return true;
    }
}

// Usage:
MyContract mc = new MyContract();
address funcAddress = mc.doSomething.address;
bytes4 funcSelector = mc.doSomething.selector;

// Old syntax (deprecated):
// mc.doSomething.gas(100000).value(1 ether)();

// New syntax:
// mc.doSomething{gas: 100000, value: 1 ether}();
```

--------------------------------

### Solidity: Optimized SSA after UnusedAssignEliminator

Source: https://docs.soliditylang.org/en/v0.8.30/internals/optimizer

Shows the optimized SSA form of the Solidity snippet after the UnusedAssignEliminator has removed assignments where the assigned value is not used.

```solidity
{
    let a_1 := 1
    let a_2 := mload(a_1)
    let a_3 := sload(a_2)
    sstore(a_3, 1)
}
```

--------------------------------

### Solidity: Array Length Read-Only and Push/Pop

Source: https://docs.soliditylang.org/en/v0.8.30/060-breaking-changes

Array member `length` is now read-only for storage arrays. Use `push()`, `push(value)`, or `pop()` for resizing. Direct assignment to `length` is disallowed to prevent storage collisions.

```Solidity
pragma solidity ^0.6.0;

contract ArrayResize {
    uint[] public myArray;

    function addElement(uint value) public {
        myArray.push(value);
    }

    function removeElement() public {
        myArray.pop();
    }

    // The following is now disallowed:
    // function resizeArray(uint newLength) public {
    //     myArray.length = newLength;
    // }
}
```

--------------------------------

### Solidity Overflow Check with Require Statements

Source: https://docs.soliditylang.org/en/v0.8.30/smtchecker

This Solidity contract includes 'require' statements to filter out potential overflow cases. By adding these checks, the SMTChecker can prove that no overflow is reachable, as demonstrated by the absence of warnings.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.0;

contract Overflow {
    uint immutable x;
    uint immutable y;

    function add(uint x_, uint y_) internal pure returns (uint) {
        return x_ + y_;
    }

    constructor(uint x_, uint y_) {
        (x, y) = (x_, y_);
    }

    function stateAdd() public view returns (uint) {
        require(x < type(uint128).max);
        require(y < type(uint128).max);
        return add(x, y);
    }
}

```

--------------------------------

### Solidity `transfer` Method Update

Source: https://docs.soliditylang.org/en/v0.8.30/080-breaking-changes

Demonstrates the required change when using the `transfer` method on an address. It now requires an explicit conversion to `address payable`.

```Solidity
payable(msg.sender).transfer(x)
```

--------------------------------

### Solidity Contract Logic Execution (delegatecall)

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Executes the code from the target address, but crucially, it also preserves the `caller` and `callvalue` of the original sender. This is often used for proxy patterns. Returns 1 on success and 0 on error.

```Solidity
bool success = delegatecall(gas, target_address, data_ptr, data_size, output_ptr, output_size);
// Example usage:
// (bool success, bytes memory returndata) = target_contract.delegatecall(abi.encodeWithSignature("functionName(uint256)", arg1));
```

--------------------------------

### Solidity Code Update: Inheritance and Overriding

Source: https://docs.soliditylang.org/en/v0.8.30/060-breaking-changes

Explains the updated rules for `virtual` and `override` keywords in Solidity for functions intended for overriding, particularly in single and multiple inheritance scenarios.

```solidity
// Add 'virtual' to functions intended to be overridden or without implementation in interfaces
contract Base {
    function foo() virtual public {
        // ...
    }
}

// Single inheritance
contract Derived1 is Base {
    function foo() override public {
        // ...
    }
}

// Multiple inheritance
contract A { function bar() virtual public; }
contract B { function bar() virtual public; }
contract Derived2 is A, B {
    function bar() override(A, B) public {
        // ...
    }
}
```

--------------------------------

### Solidity: Keccak256 Hash

Source: https://docs.soliditylang.org/en/v0.8.30/units-and-global-variables

Computes the Keccak-256 hash of the input bytes. The alias 'sha3' was removed in version 0.5.0.

```Solidity
keccak256(bytes memory) returns (bytes32)
```

--------------------------------

### Solidity Byte Array Manipulation

Source: https://docs.soliditylang.org/en/v0.8.30/types

Illustrates operations on byte arrays (`bytes`) in Solidity. Byte arrays are stored without padding and can be manipulated similarly to `uint8[]`. This includes appending elements with `push()`, assigning values to specific indices, and deleting elements.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

contract ArrayContract {
    bytes byteData;

    function byteArrays(bytes memory data) public {
        // byte arrays ("bytes") are different as they are stored without padding,
        // but can be treated identical to "uint8[]"
        byteData = data;
        for (uint i = 0; i < 7)
            byteData.push();
        byteData[3] = 0x08;
        delete byteData[2];
    }
}

```

--------------------------------

### Solidity: Replace `now` with `block.timestamp`

Source: https://docs.soliditylang.org/en/v0.8.30/070-breaking-changes

Demonstrates the change from the deprecated `now` keyword to the current `block.timestamp` in Solidity. This ensures code compatibility with newer versions.

```solidity
Change `now` to `block.timestamp`.
```

--------------------------------

### Vulnerable Withdraw Function in Solidity using Send

Source: https://docs.soliditylang.org/en/v0.8.30/security-considerations

This Solidity code snippet demonstrates a vulnerable contract function that allows reentrancy due to the use of `send` for transferring Ether.  The recipient can call back into the contract before the state is updated, potentially allowing multiple withdrawals. Requires Solidity version >=0.6.0 and <0.9.0.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

// THIS CONTRACT CONTAINS A BUG - DO NOT USE
contract Fund {
    /// @dev Mapping of ether shares of the contract.
    mapping(address => uint) shares;
    /// Withdraw your share.
    function withdraw() public {
        if (payable(msg.sender).send(shares[msg.sender]))
            shares[msg.sender] = 0;
    }
}

```

--------------------------------

### Solidity Block and Transaction Properties

Source: https://docs.soliditylang.org/en/v0.8.30/units-and-global-variables

Access properties of the current block and transaction within Solidity smart contracts. These include block number, timestamp, base fee, gas limit, sender address, value, and origin.

```solidity
uint blockNumber = block.number;
address coinbase = block.coinbase;
uint timestamp = block.timestamp;
address sender = msg.sender;
uint value = msg.value;
address origin = tx.origin;
```

--------------------------------

### Solidity Base Fee (basefee)

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Returns the current block's base fee, as defined by EIP-1559. This value is used in gas price calculations for EIP-1559 compliant transactions.

```Solidity
uint256 baseFee = basefee();
```

--------------------------------

### Solidity Arithmetic Operations with `unchecked`

Source: https://docs.soliditylang.org/en/v0.8.30/080-breaking-changes

Shows how to use the `unchecked` block in Solidity to bypass overflow/underflow checks for arithmetic operations, potentially improving gas efficiency.

```Solidity
unchecked {
  x.add(y);
}
```

--------------------------------

### Solidity Reentrancy Guard using Transient Storage

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

This Solidity code demonstrates a reentrancy guard pattern using transient storage and a custom modifier. It prevents a contract from being re-entered within the same transaction. Requires EVM version 'cancun' or newer.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.28;

contract Generosity {
    mapping(address => bool) sentGifts;
    bool transient locked;

    modifier nonReentrant {
        require(!locked, "Reentrancy attempt");
        locked = true;
        _;
        // Unlocks the guard, making the pattern composable.
        // After the function exits, it can be called again, even in the same transaction.
        locked = false;
    }

    function claimGift() nonReentrant public {
        require(address(this).balance >= 1 ether);
        require(!sentGifts[msg.sender]);
        (bool success, ) = msg.sender.call{value: 1 ether}("");
        require(success);

        // In a reentrant function, doing this last would open up the vulnerability
        sentGifts[msg.sender] = true;
    }
}

```

--------------------------------

### ABI Encoding of Strings in a Dynamic Array (Solidity)

Source: https://docs.soliditylang.org/en/v0.8.30/abi-spec

Demonstrates the ABI encoding of individual strings within a dynamic array in Solidity. Each string's encoding includes its length (as a count of characters) followed by its UTF-8 representation, padded to 32 bytes. This is crucial for understanding how dynamic string data is handled in smart contracts.

```text
0x0000000000000000000000000000000000000000000000000000000000000003 - count for "one"
0x6f6e650000000000000000000000000000000000000000000000000000000000 - encoding of "one"
0x0000000000000000000000000000000000000000000000000000000000000003 - count for "two"
0x74776f0000000000000000000000000000000000000000000000000000000000 - encoding of "two"
0x0000000000000000000000000000000000000000000000000000000000000005 - count for "three"
0x7468726565000000000000000000000000000000000000000000000000000000 - encoding of "three"
```

--------------------------------

### Solidity Block Difficulty (difficulty)

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Returns the difficulty of the current block. Note: This opcode is disallowed in EVM versions >= Paris and has been renamed to `prevrandao`. Its semantics may differ based on the EVM version and chain.

```Solidity
uint256 blockDifficulty = difficulty();
```

--------------------------------

### Solidity: Storage Pointer Variable Access

Source: https://docs.soliditylang.org/en/v0.8.30/070-breaking-changes

Updates the syntax for accessing the slot and offset of storage pointer variables. Instead of `x_slot` and `x_offset`, use `x.slot` and `x.offset` for clarity and consistency.

```Solidity
assembly {
    // let slot := x_slot // Old syntax
    let slot := x.slot // New syntax
    // let offset := x_offset // Old syntax
    let offset := x.offset // New syntax
}
```

--------------------------------

### Solidity: Override External Function with Public State Variable

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Demonstrates how a public state variable can override an external function. The parameter and return types of the function must match the getter function of the state variable for this to be valid.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

contract A
{
    function f() external view virtual returns(uint) { return 5; }
}

contract B is A
{
    uint public override f;
}

```

--------------------------------

### Command-Line Option Renaming: `--julia` to `--yul` (Solidity Compiler)

Source: https://docs.soliditylang.org/en/v0.8.30/050-breaking-changes

The Solidity compiler's command-line option `--julia` has been renamed to `--yul`. This change reflects the renaming of the intermediate language from Julia to Yul, ensuring consistency in terminology.

```Shell
# Compiling with Yul output using the new option
solc --yul MyContract.sol

# The previous option is now deprecated/removed
# solc --julia MyContract.sol
```

--------------------------------

### Solidity: Test double state variable declaration

Source: https://docs.soliditylang.org/en/v0.8.30/contributing

This Solidity code snippet demonstrates a syntax test case where a state variable is declared twice, intentionally causing a DeclarationError. It includes the contract code, a separator, and the expected error message with its location.

```solidity
contract test {
    uint256 variable;
    uint128 variable;
}
// ----
// DeclarationError: (36-52): Identifier already declared.

```

--------------------------------

### Solidity: Repeat `using for` statements in derived contracts

Source: https://docs.soliditylang.org/en/v0.8.30/070-breaking-changes

Highlights the requirement to repeat `using A for B` statements in all derived contracts if necessary in Solidity. This ensures that extensions are correctly applied throughout the inheritance hierarchy.

```solidity
Repeat the `using A for B` statements in all derived contracts if needed.
```

--------------------------------

### Solidity: Fallback and Receive Ether Functions

Source: https://docs.soliditylang.org/en/v0.8.30/060-breaking-changes

The unnamed fallback function is split into `fallback()` and `receive()`. `receive()` handles empty calldata and ether reception (implicitly payable). `fallback()` handles non-matching calls and can be made `payable`.

```Solidity
pragma solidity ^0.6.0;

contract EtherReceiver {
    event Received(address sender, uint amount);
    event Fallbacked(bytes data);

    receive() external payable {
        emit Received(msg.sender, msg.value);
    }

    fallback() external {
        emit Fallbacked(msg.data);
    }
}
```

--------------------------------

### Inline Functions in Expressions (Solidity)

Source: https://docs.soliditylang.org/en/v0.8.30/internals/optimizer

The ExpressionInliner performs restricted function inlining for functions within functional expressions. It targets functions returning a single value with a body like `r := <functional expression>`, where neither the function nor `r` are referenced in the RHS. Arguments must be movable, and referenced less than twice or cheap. The result is a single expression. Requires unique source names.

--------------------------------

### Solidity: Try/Catch for External Calls

Source: https://docs.soliditylang.org/en/v0.8.30/060-breaking-changes

Introduces the `try/catch` statement to handle potential failures in external contract calls. This allows for more robust error handling and recovery mechanisms.

```Solidity
pragma solidity ^0.6.0;

interface IERC20 {
    function transfer(address to, uint256 amount) external returns (bool);
}

contract Caller {
    IERC20 token;

    constructor(address tokenAddress) {
        token = IERC20(tokenAddress);
    }

    function callTokenTransfer(address to, uint256 amount) public {
        try token.transfer(to, amount) {
            // Handle success
        } catch (bytes memory error) {
            // Handle failure
            // For example, re-throw or log the error
            revert(error);
        }
    }
}
```

--------------------------------

### Integer Operators in Solidity

Source: https://docs.soliditylang.org/en/v0.8.30/types

Covers the arithmetic, comparison, bitwise, and shift operators for integer types in Solidity. Integers can be signed ('int') or unsigned ('uint') with sizes from 8 to 256 bits. Arithmetic operations are checked by default, reverting on overflow, but can be performed in 'unchecked' blocks.

```Solidity
// Comparisons
intVariable <= anotherIntVariable;

// Bitwise operations
intVariable & anotherIntVariable; // Bitwise AND
intVariable | anotherIntVariable; // Bitwise OR
intVariable ^ anotherIntVariable; // Bitwise XOR
~intVariable;                   // Bitwise NOT

// Shift operations
intVariable << uintVariable; // Left shift
intVariable >> uintVariable; // Right shift

// Arithmetic operations
intVariable + anotherIntVariable;
intVariable - anotherIntVariable;
-intVariable; // Unary minus (signed integers only)
intVariable * anotherIntVariable;
intVariable / anotherIntVariable;
intVariable % anotherIntVariable; // Modulo
intVariable ** anotherIntVariable; // Exponentiation
```

--------------------------------

### Solidity Event Declaration and Emission

Source: https://docs.soliditylang.org/en/v0.8.30/structure-of-a-contract

Declares an event 'HighestBidIncreased' to log bidder and amount, and emits this event within the 'bid' function. Events provide an interface to EVM logging facilities.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.22;

event HighestBidIncreased(address bidder, uint amount); // Event

contract SimpleAuction {
    function bid() public payable {
        // ...
        emit HighestBidIncreased(msg.sender, msg.value); // Triggering event
    }
}

```

--------------------------------

### Annotate Assembly Block as Memory-Safe (Solidity)

Source: https://docs.soliditylang.org/en/v0.8.30/assembly

This code snippet demonstrates how to annotate an inline assembly block in Solidity to indicate that it adheres to the compiler's memory model. This allows for optimizations by the Yul IR code generation pipeline.

```solidity
assembly ("memory-safe") {
    ...
}
```

--------------------------------

### Solidity Indexed Event Parameter Encoding: Bytes and String

Source: https://docs.soliditylang.org/en/v0.8.30/abi-spec

Defines the encoding for indexed event parameters of type bytes and string. The encoding is simply the string contents without any padding or length prefix.

```Solidity
encoding of a `bytes` and `string` value is just the string contents without any padding or length prefix
```

--------------------------------

### Solidity String Literal with Escape Characters

Source: https://docs.soliditylang.org/en/v0.8.30/types

Demonstrates the use of various escape characters within a Solidity string literal, including newlines, quotes, and backslashes. String literals can be split across lines.

```Solidity
"\n\"'\\abc\ndef"
```

--------------------------------

### Solidity Transaction Gas Price (gasprice)

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Returns the gas price of the current transaction. This is the amount of wei paid per unit of gas.

```Solidity
uint256 gasPrice = gasprice();
```

--------------------------------

### Solidity: Type Information for Interfaces

Source: https://docs.soliditylang.org/en/v0.8.30/units-and-global-variables

Retrieves the EIP-165 interface identifier for a given interface type `I` using `type(I).interfaceId`. This identifier is calculated as the XOR of all function selectors within the interface, excluding inherited ones.

```Solidity
type(I).interfaceId
```

--------------------------------

### EVM Dialect Byte Manipulation and Shift Opcodes

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Facilitates byte extraction and bit shifting operations. The 'byte' function retrieves a specific byte from a 256-bit word, while 'shl', 'shr', and 'sar' perform logical left, logical right, and arithmetic right shifts respectively.

```solidity
byte(n, x)
shl(x, y)
shr(x, y)
sar(x, y)
signextend(i, x)
```

--------------------------------

### Solidity Division by Zero Handling

Source: https://docs.soliditylang.org/en/v0.8.30/types

Highlights that division by zero in Solidity triggers a Panic error and this behavior cannot be disabled using `unchecked` blocks.

```solidity
// Division by zero causes a Panic error. This check can **not** be disabled through `unchecked { ... }`.
```

--------------------------------

### Solidity: Override Modifier with Multiple Inheritance

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Illustrates overriding a modifier inherited from multiple base contracts. In multiple inheritance, all direct base contracts that define the same modifier must be explicitly specified after the 'override' keyword.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

contract Base1
{
    modifier foo() virtual {_;}
}

contract Base2
{
    modifier foo() virtual {_;}
}

contract Inherited is Base1, Base2
{
    modifier foo() override(Base1, Base2) {_;}
}

```

--------------------------------

### JSON AST Field Changes: `constant`, `payable`, `isConstructor` (Solidity)

Source: https://docs.soliditylang.org/en/v0.8.30/050-breaking-changes

The Solidity compiler's JSON Abstract Syntax Tree (AST) has undergone changes. The `constant` and `payable` fields are removed, with their information now consolidated in the `stateMutability` field. `isConstructor` is replaced by `kind` with specific values like "constructor", "fallback", or "function".

```JSON
// Example of a FunctionDefinition node in JSON AST (Solidity < 0.8.30)
{
  "nodeType": "FunctionDefinition",
  "name": "myFunction",
  "constant": false,
  "payable": true,
  "isConstructor": false,
  "stateMutability": "payable"
}

// Example of a FunctionDefinition node in JSON AST (Solidity >= 0.8.30)
{
  "nodeType": "FunctionDefinition",
  "name": "myFunction",
  "kind": "function",
  "stateMutability": "payable"
}
```

--------------------------------

### Solidity: Dangling reference from pop() and push() on storage array

Source: https://docs.soliditylang.org/en/v0.8.30/types

Demonstrates a dangling reference in Solidity by storing a reference to a storage array's last element, popping the element, and then writing to the reference. This operation bypasses reverts and can lead to unexpected data in subsequent array operations.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.0 <0.9.0;

contract C {
    uint[][] s;

    function f() public {
        // Stores a pointer to the last array element of s.
        uint[] storage ptr = s[s.length - 1];
        // Removes the last array element of s.
        s.pop();
        // Writes to the array element that is no longer within the array.
        ptr.push(0x42);
        // Adding a new element to ``s`` now will not add an empty array, but
        // will result in an array of length 1 with ``0x42`` as element.
        s.push();
        assert(s[s.length - 1][0] == 0x42);
    }
}

```

--------------------------------

### Solidity: Convert Negative Int to Unsigned Int

Source: https://docs.soliditylang.org/en/v0.8.30/types

Demonstrates explicit conversion of a negative signed integer to an unsigned integer type. This conversion uses two's complement representation for negative numbers, potentially leading to unexpected large positive values.

```solidity
int  y = -3;
uint x = uint(y);

```

--------------------------------

### Reachability Assertion for Robot Contract - Solidity

Source: https://docs.soliditylang.org/en/v0.8.30/smtchecker

Adds a specific assertion to the Robot contract to check if the position (2, 4) is unreachable. This function is used to test the SMTChecker's ability to find counterexamples for reachability.

```Solidity
function reach_2_4() public view {
    assert(!(x == 2 && y == 4));
}

```

--------------------------------

### Solidity: Address and uint type conversion

Source: https://docs.soliditylang.org/en/v0.8.30/080-breaking-changes

Conversions between `address` and `uint` types have been restricted due to changes in both type-category and width. Use intermediate conversions like `address(uint160(uint))` or `uint(uint160(address))`.

```Solidity
address(uint)
```

```Solidity
uint(address)
```

```Solidity
address(uint160(uint))
```

```Solidity
uint(uint160(address))
```

--------------------------------

### Solidity Indexed Event Parameter Encoding: Array

Source: https://docs.soliditylang.org/en/v0.8.30/abi-spec

Details the encoding for indexed event parameters that are arrays (dynamic or static). The encoding is the concatenation of the elements' encodings, always padded to a multiple of 32 bytes, without any length prefix.

```Solidity
the encoding of an array (both dynamically- and statically-sized) is the concatenation of the encoding of its elements, always padded to a multiple of 32 bytes (even `bytes` and `string`) and without any length prefix
```

--------------------------------

### Solidity Block Hash (blockhash)

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Returns the hash of a specific block. It only works for the last 256 blocks, excluding the current one. Providing a block number outside this range will result in a hash of zero.

```Solidity
bytes32 blockHash = blockhash(block_number);
```

--------------------------------

### Solidity Miner/Coinbase Address (coinbase)

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Returns the address of the current mining beneficiary (coinbase). This is the address that receives block rewards.

```Solidity
address coinbaseAddress = coinbase();
```

--------------------------------

### Vulnerable Withdraw Function in Solidity using Call

Source: https://docs.soliditylang.org/en/v0.8.30/security-considerations

This Solidity code snippet shows another vulnerable function that allows reentrancy through the `call` function. `call` forwards all remaining gas, making the contract more susceptible to reentrancy attacks.  Requires Solidity version >=0.6.2 and <0.9.0.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.2 <0.9.0;

// THIS CONTRACT CONTAINS A BUG - DO NOT USE
contract Fund {
    /// @dev Mapping of ether shares of the contract.
    mapping(address => uint) shares;
    /// Withdraw your share.
    function withdraw() public {
        (bool success,) = msg.sender.call{value: shares[msg.sender]}("");
        if (success)
            shares[msg.sender] = 0;
    }
}

```

--------------------------------

### Solidity Blob Base Fee (blobbasefee)

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Returns the current block's blob base fee, as defined by EIP-4844 (Proto-Danksharding). This is relevant for transactions that include data blobs.

```Solidity
uint256 blobBaseFee = blobbasefee();
```

--------------------------------

### Solidity: Recommended explicit conversion for uint(-1)

Source: https://docs.soliditylang.org/en/v0.8.30/080-breaking-changes

In Solidity 0.8.30, explicit conversions from negative literals or literals exceeding uint160.max to address are disallowed. Use `type(uint).max` instead of `uint(-1)` for unsigned integer types.

```Solidity
uint(-1)
```

```Solidity
type(uint).max
```

--------------------------------

### Solidity: Unicode String Literals

Source: https://docs.soliditylang.org/en/v0.8.30/070-breaking-changes

Enables the use of Unicode string literals with the `unicode` prefix, allowing for valid UTF-8 sequences within strings. This improves internationalization and the ability to represent a wider range of characters.

```Solidity
unicode"Hello 😃"
```

--------------------------------

### Annotate Assembly Block as Memory-Safe via Comment (Solidity)

Source: https://docs.soliditylang.org/en/v0.8.30/assembly

This Solidity code shows an alternative way to mark an assembly block as memory-safe using a special comment, intended for backward compatibility with older compiler versions.

```solidity
/// @solidity memory-safe-assembly
assembly {
    ...
}
```

--------------------------------

### Solidity ABI: Static Type Encoding

Source: https://docs.soliditylang.org/en/v0.8.30/abi-spec

Describes the encoding of static types in the Solidity ABI, where data is encoded in-place and padded to 32 bytes. This includes integer types, addresses, booleans, and fixed-point numbers.

```Solidity
uint<M>: enc(X) is the big-endian encoding of X, padded on the higher-order (left) side with zero-bytes such that the length is 32 bytes.
address: as in the uint160 case
int<M>: enc(X) is the big-endian two’s complement encoding of X, padded on the higher-order (left) side with 0xff bytes for negative X and with zero-bytes for non-negative X such that the length is 32 bytes.
bool: as in the uint8 case, where 1 is used for true and 0 for false
fixed<M>x<N>: enc(X) is enc(X * 10**N) where X * 10**N is interpreted as a int256.
fixed: as in the fixed128x18 case
ufixed<M>x<N>: enc(X) is enc(X * 10**N) where X * 10**N is interpreted as a uint256.
ufixed: as in the ufixed128x18 case
bytes<M>: enc(X) is the sequence of bytes in X padded with trailing zero-bytes to a length of 32 bytes.
```

--------------------------------

### Solidity ABI: Dynamic Type Encoding

Source: https://docs.soliditylang.org/en/v0.8.30/abi-spec

Explains the encoding of dynamic types in the Solidity ABI, such as bytes, strings, and arrays. These types are encoded at a separate location and referenced by an offset.

```Solidity
bytes: enc(X) = enc(k) pad_right(X), i.e. the number of bytes is encoded as a uint256 followed by the actual value of X as a byte sequence, followed by the minimum number of zero-bytes such that len(enc(X)) is a multiple of 32.
string: enc(X) = enc(enc_utf8(X)), i.e. X is UTF-8 encoded and this value is interpreted as of bytes type and encoded further. Note that the length used in this subsequent encoding is the number of bytes of the UTF-8 encoded string, not its number of characters.
```

--------------------------------

### Solidity: Override and Abstract Contract Syntax

Source: https://docs.soliditylang.org/en/v0.8.30/060-breaking-changes

Functions can only be overridden if marked `virtual` or defined in an interface. New `override` keyword required, with optional base listing. Abstract contracts must implement all functions and are marked with `abstract`.

```Solidity
pragma solidity ^0.6.0;

contract Base {
    function doSomething() virtual public {
        // ...
    }
}

contract Derived is Base {
    function doSomething() override public {
        // ...
    }
}

abstract contract MyAbstractContract {
    function virtualFunction() virtual public;
}

contract ConcreteContract is MyAbstractContract {
    function virtualFunction() public {
        // ...
    }
}
```

--------------------------------

### Solidity: Prevent tx.origin Authorization Vulnerability

Source: https://docs.soliditylang.org/en/v0.8.30/security-considerations

Demonstrates a common vulnerability in Solidity where using tx.origin for authorization can be exploited. The correct approach is to use msg.sender for authorization to prevent attacks.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;
// THIS CONTRACT CONTAINS A BUG - DO NOT USE
contract TxUserWallet {
    address owner;

    constructor() {
        owner = msg.sender;
    }

    function transferTo(address payable dest, uint amount) public {
        // THE BUG IS RIGHT HERE, you must use msg.sender instead of tx.origin
        require(tx.origin == owner);
        dest.transfer(amount);
    }
}

```

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;
interface TxUserWallet {
    function transferTo(address payable dest, uint amount) external;
}

contract TxAttackWallet {
    address payable owner;

    constructor() {
        owner = payable(msg.sender);
    }

    receive() external payable {
        TxUserWallet(msg.sender).transferTo(owner, msg.sender.balance);
    }
}

```

--------------------------------

### Solidity: Convert Dynamic Bytes to Fixed-Size Bytes

Source: https://docs.soliditylang.org/en/v0.8.30/types

Shows explicit conversion of dynamic `bytes` arrays and `calldata` slices to fixed-size byte types. Truncation occurs if the source is longer than the target; padding with zeros occurs if it's shorter.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.5;

contract C {
    bytes s = "abcdefgh";
    function f(bytes calldata c, bytes memory m) public view returns (bytes16, bytes3) {
        require(c.length == 16, "");
        bytes16 b = bytes16(m);  // if length of m is greater than 16, truncation will happen
        b = bytes16(s);  // padded on the right, so result is "abcdefgh\0\0\0\0\0\0\0\0"
        bytes3 b1 = bytes3(s); // truncated, b1 equals to "abc"
        b = bytes16(c[:8]);  // also padded with zeros
        return (b, b1);
    }
}

```

--------------------------------

### Solidity: Inline Assembly Keyword Usage

Source: https://docs.soliditylang.org/en/v0.8.30/060-breaking-changes

Opcodes without arguments in inline assembly are now represented as built-in functions (e.g., `gas()` instead of `gas`). Variable names ending in `_slot` or `_offset` are disallowed.

```Solidity
pragma solidity ^0.6.0;

contract AssemblyKeywords {
    function getGas() public pure returns (uint) {
        uint gasAmount;
        assembly {
            gasAmount := gas() // Use gas() instead of standalone gas
        }
        return gasAmount;
    }
}
```

--------------------------------

### Solidity: Unsoundness with Trusted External Calls and Type Casting

Source: https://docs.soliditylang.org/en/v0.8.30/smtchecker

Illustrates an unsound scenario in Solidity where treating external calls as trusted, combined with casting addresses between different contract types, can lead to incorrect SMTChecker analysis results. This occurs because the checker may not correctly track storage changes across different perceived contract types.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.0;

contract D {
    constructor(uint _x) { x = _x; }
    uint public x;
    function setX(uint _x) public { x = _x; }
}

contract E {
    constructor() { x = 2; }
    uint public x;
    function setX(uint _x) public { x = _x; }
}

contract C {
    function f() public {
        address d = address(new D(42));

        // `d` was deployed as `D`, so its `x` should be 42 now.
        assert(D(d).x() == 42); // should hold
        assert(D(d).x() == 43); // should fail

        // E and D have the same interface, so the following
        // call would also work at runtime.
        // However, the change to `E(d)` is not reflected in `D(d)`.
        E(d).setX(1024);

        // Reading from `D(d)` now will show old values.
        // The assertion below should fail at runtime,
        // but succeeds in this mode's analysis (unsound).
        assert(D(d).x() == 42);
        // The assertion below should succeed at runtime,
        // but fails in this mode's analysis (false positive).
        assert(D(d).x() == 1024);
    }
}

```

--------------------------------

### Solidity ABI: Function Call Encoding

Source: https://docs.soliditylang.org/en/v0.8.30/abi-spec

Specifies the structure of a function call in the Solidity ABI, which includes the function selector and the encoded arguments.

```Solidity
function_selector(f) enc((a_1, ..., a_n))
```

--------------------------------

### Solidity: Use unchecked for wrapping arithmetic behavior

Source: https://docs.soliditylang.org/en/v0.8.30/080-breaking-changes

Demonstrates how to revert to the previous wrapping behavior for arithmetic operations in Solidity by using the `unchecked` block. This is useful when default overflow/underflow checks are not desired.

```Solidity
pragma solidity ^0.8.0;

contract Example {
    function addWithWrapping(uint a, uint b) public pure returns (uint) {
        // Previous wrapping behavior
        unchecked {
            return a + b;
        }
    }
}
```

--------------------------------

### Solidity ABI: Function Return Value Encoding

Source: https://docs.soliditylang.org/en/v0.8.30/abi-spec

Defines how function return values are encoded in the Solidity ABI, where multiple return values are combined into a tuple and then encoded.

```Solidity
enc((v_1, ..., v_k))
```

--------------------------------

### Solidity Indexed Event Parameter Encoding: Struct

Source: https://docs.soliditylang.org/en/v0.8.30/abi-spec

Specifies the encoding for indexed event parameters that are structs. The encoding is the concatenation of the members' encodings, always padded to a multiple of 32 bytes, including bytes and string members.

```Solidity
the encoding of a struct is the concatenation of the encoding of its members, always padded to a multiple of 32 bytes (even `bytes` and `string`)
```

--------------------------------

### Two-Dimensional Array Literals with Explicit Types in Solidity

Source: https://docs.soliditylang.org/en/v0.8.30/types

Demonstrates the creation of two-dimensional array literals, emphasizing the need for explicit type casting for elements to ensure a common base type for all sub-arrays.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract C {
    function f() public pure returns (uint24[2][4] memory) {
        uint24[2][4] memory x = [[uint24(0x1), 1], [0xffffff, 2], [0xff, 3], [0xffff, 4]];
        // The following does not work, because some of the inner arrays are not of the right type.
        // uint[2][4] memory x = [[0x1, 1], [0xffffff, 2], [0xff, 3], [0xffff, 4]];
        return x;
    }
}

```

--------------------------------

### Solidity Exponentiation Associativity

Source: https://docs.soliditylang.org/en/v0.8.30/080-breaking-changes

Explains the change in how exponentiation operations are evaluated in Solidity, requiring explicit grouping for clarity and correctness.

```Solidity
(x**y)**z
```

--------------------------------

### Solidity: Truncate Bytes Sequence on Fixed-Size Bytes Conversion

Source: https://docs.soliditylang.org/en/v0.8.30/types

Explains how converting a larger fixed-size bytes type to a smaller one truncates the byte sequence from the end. The resulting bytes type retains the initial bytes of the original sequence.

```solidity
bytes2 a = 0x1234;
bytes1 b = bytes1(a); // b will be 0x12

```

--------------------------------

### Solidity ABI: Array and Tuple Encoding

Source: https://docs.soliditylang.org/en/v0.8.30/abi-spec

Details how arrays and tuples are encoded in the Solidity ABI. Arrays are treated as tuples, and tuples are encoded by concatenating the encoded heads and tails of their elements.

```Solidity
T[k] for any T and k: enc(X) = enc((X[0], ..., X[k-1])) i.e. it is encoded as if it were a tuple with k elements of the same type.
T[] where X has k elements (k is assumed to be of type uint256): enc(X) = enc(k) enc((X[0], ..., X[k-1])) i.e. it is encoded as if it were a tuple with k elements of the same type (resp. an array of static size k), prefixed with the number of elements.
(T1,...,Tk) for k >= 0 and any types T1, ..., Tk
enc(X) = head(X(1)) ... head(X(k)) tail(X(1)) ... tail(X(k))
where X = (X(1), ..., X(k)) and head and tail are defined for Ti as follows:
if Ti is static: head(X(i)) = enc(X(i)) and tail(X(i)) = "" (the empty string)
otherwise, i.e. if Ti is dynamic:
head(X(i)) = enc(len( head(X(1)) ... head(X(k)) tail(X(1)) ... tail(X(i-1)) )) tail(X(i)) = enc(X(i))
```

--------------------------------

### Solidity: Struct and Enum at File Level

Source: https://docs.soliditylang.org/en/v0.8.30/060-breaking-changes

Allows declaration of `struct` and `enum` types at the file level, outside of contract definitions. This promotes better code organization and reusability.

```Solidity
pragma solidity ^0.6.0;

enum State { Initial, Active, Finalized };

struct Item {
    uint id;
    string name;
    State currentState;
}

contract Manager {
    Item public myItem;

    function createItem(uint id, string memory name) public {
        myItem = Item(id, name, State.Initial);
    }
}
```

--------------------------------

### Explicit Data Location for Variables and Parameters (Solidity)

Source: https://docs.soliditylang.org/en/v0.8.30/050-breaking-changes

Solidity 0.8.30 mandates explicit data locations (e.g., `memory`, `storage`, `calldata`) for struct, array, and mapping types, including function parameters and return variables. This prevents potential errors and clarifies data handling. External functions require `calldata` for parameters.

```Solidity
pragma solidity ^0.8.30;

contract DataLocation {
    uint[] storage myArray;

    function setArray(uint[] memory _array) public {
        myArray = _array;
    }

    function getArray() public view returns (uint[] storage) {
        return myArray;
    }

    // External function requires calldata for parameters
    function processExternalData(uint[] calldata _data) external {
        // ...
    }
}
```

--------------------------------

### Solidity Custom Error Definition and Usage

Source: https://docs.soliditylang.org/en/v0.8.30/structure-of-a-contract

Defines a custom error 'NotEnoughFunds' with specific data fields and uses it in a 'revert' statement within the 'transfer' function to handle insufficient balance scenarios. Custom errors are gas-efficient alternatives to string reverts.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.4;

/// Not enough funds for transfer. Requested `requested`,
/// but only `available` available.
error NotEnoughFunds(uint requested, uint available);

contract Token {
    mapping(address => uint) balances;
    function transfer(address to, uint amount) public {
        uint balance = balances[msg.sender];
        if (balance < amount)
            revert NotEnoughFunds(amount, balance);
        balances[msg.sender] -= amount;
        balances[to] += amount;
        // ...
    }
}

```

--------------------------------

### Solidity: Truncate Higher-Order Bits on Integer Conversion

Source: https://docs.soliditylang.org/en/v0.8.30/types

Illustrates explicit conversion of a larger integer type to a smaller one, where higher-order bits are truncated. The resulting value is determined by the lower-order bits that fit into the target type.

```solidity
uint32 a = 0x12345678;
uint16 b = uint16(a); // b will be 0x5678 now

```

--------------------------------

### Solidity Array Clearing with delete and Re-initialization

Source: https://docs.soliditylang.org/en/v0.8.30/types

Shows two methods for completely clearing arrays in Solidity. The `delete` keyword removes all elements from both dynamic and fixed-size arrays. Alternatively, a dynamic array can be cleared by re-initializing it with a new array of size zero.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

contract ArrayContract {
    uint[2**20] aLotOfIntegers;
    bool[2][] pairsOfFlags;

    function clear() public {
        // these clear the arrays completely
        delete pairsOfFlags;
        delete aLotOfIntegers;
        // identical effect here
        pairsOfFlags = new bool[2][](0);
    }
}

```

--------------------------------

### Solidity Modulo by Zero Handling

Source: https://docs.soliditylang.org/en/v0.8.30/types

States that the modulo operation with zero as the divisor causes a Panic error in Solidity, and this check cannot be bypassed with `unchecked` blocks.

```solidity
// Modulo with zero causes a Panic error. This check can **not** be disabled through `unchecked { ... }`.
```

--------------------------------

### ForLoopConditionOutOfBody - Transformation 1

Source: https://docs.soliditylang.org/en/v0.8.30/internals/optimizer

Transforms a 'for' loop by moving the condition out of the loop body. This applies when the condition is `iszero(c)` and the loop uses a `break` statement.

```Solidity
for { ... } 1 { ... } {
if iszero(c) { break }
...
}
```

```Solidity
for { ... } c { ... } {
...
}
```

--------------------------------

### Encoding of Nested Dynamic Arrays and Strings in Solidity

Source: https://docs.soliditylang.org/en/v0.8.30/abi-spec

Illustrates the ABI encoding for a Solidity function with nested dynamic arrays (uint256[][]) and dynamic arrays of strings (string[]). It details the encoding of array lengths, elements, and offsets for nested structures.

```text
Encoding for [1, 2]:
  0000000000000000000000000000000000000000000000000000000000000002
  0000000000000000000000000000000000000000000000000000000000000001
  0000000000000000000000000000000000000000000000000000000000000002

Encoding for [3]:
  0000000000000000000000000000000000000000000000000000000000000001
  0000000000000000000000000000000000000000000000000000000000000003

Offset calculation for [[1, 2], [3]]:
Line 0: a (offset of [1, 2])
Line 1: b (offset of [3])
Line 2: 0000000000000000000000000000000000000000000000000000000000000002 - count for [1, 2]
Line 3: 0000000000000000000000000000000000000000000000000000000000000001 - encoding of 1
Line 4: 0000000000000000000000000000000000000000000000000000000000000002 - encoding of 2
Line 5: 0000000000000000000000000000000000000000000000000000000000000001 - count for [3]
Line 6: 0000000000000000000000000000000000000000000000000000000000000003 - encoding of 3

Offset a = 0x0000000000000000000000000000000000000000000000000000000000000040
```

--------------------------------

### Solidity: Address Payable Conversion

Source: https://docs.soliditylang.org/en/v0.8.30/060-breaking-changes

Allows explicit conversion from `address` to `address payable` using `payable(x)`, where `x` must be of type `address`. This is useful for sending ether.

```Solidity
pragma solidity ^0.6.0;

contract PayableConversion {
    address payable public owner;

    constructor() {
        // Assigning the deployer's address, which is implicitly payable in the constructor context
        owner = payable(msg.sender);
    }

    function sendToOwner(uint amount) public {
        // Explicitly convert owner address to payable before sending
        payable(owner).transfer(amount);
    }
}
```

--------------------------------

### Solidity: Contract with External Call - Default Behavior

Source: https://docs.soliditylang.org/en/v0.8.30/smtchecker

Demonstrates a Solidity contract making an external call to another contract. By default, the SMTChecker treats external calls as untrusted, potentially issuing warnings if assertions depend on the external contract's state.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.0;

contract Ext {
    uint public x;
    function setX(uint _x) public { x = _x; }
}
contract MyContract {
    function callExt(Ext _e) public {
        _e.setX(42);
        assert(_e.x() == 42);
    }
}

```

--------------------------------

### Solidity: Bytes and int type conversion

Source: https://docs.soliditylang.org/en/v0.8.30/080-breaking-changes

Conversions between byte arrays and signed integers are restricted due to changes in type-category and sign. Use intermediate `uint` conversions.

```Solidity
int80(bytes10)
```

```Solidity
bytes10(int80)
```

```Solidity
int80(uint80(bytes10))
```

```Solidity
bytes10(uint80(int80))
```

--------------------------------

### Solidity Contract for Access Restriction

Source: https://docs.soliditylang.org/en/v0.8.30/common-patterns

This Solidity contract demonstrates various access restriction patterns using function modifiers. It includes modifiers for restricting calls by a specific address (`onlyBy`), by time (`onlyAfter`), and by required Ether amount (`costs`). It also defines custom errors for unauthorized access, early function calls, and insufficient Ether.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.4;

contract AccessRestriction {
    // These will be assigned at the construction
    // phase, where `msg.sender` is the account
    // creating this contract.
    address public owner = msg.sender;
    uint public creationTime = block.timestamp;

    // Now follows a list of errors that
    // this contract can generate together
    // with a textual explanation in special
    // comments.

    /// Sender not authorized for this
    /// operation.
    error Unauthorized();

    /// Function called too early.
    error TooEarly();

    /// Not enough Ether sent with function call.
    error NotEnoughEther();

    // Modifiers can be used to change
    // the body of a function.
    // If this modifier is used, it will
    // prepend a check that only passes
    // if the function is called from
    // a certain address.
    modifier onlyBy(address account)
    {
        if (msg.sender != account)
            revert Unauthorized();
        // Do not forget the "_"; It will
        // be replaced by the actual function
        // body when the modifier is used.
        _;
    }

    /// Make `newOwner` the new owner of this
    /// contract.
    function changeOwner(address newOwner)
        public
        onlyBy(owner)
    {
        owner = newOwner;
    }

    modifier onlyAfter(uint time) {
        if (block.timestamp < time)
            revert TooEarly();
        _;
    }

    /// Erase ownership information.
    /// May only be called 6 weeks after
    /// the contract has been created.
    function disown()
        public
        onlyBy(owner)
        onlyAfter(creationTime + 6 weeks)
    {
        delete owner;
    }

    // This modifier requires a certain
    // fee being associated with a function call.
    // If the caller sent too much, he or she is
    // refunded, but only after the function body.
    // This was dangerous before Solidity version 0.4.0, 
    // where it was possible to skip the part after `_;`.
    modifier costs(uint amount) {
        if (msg.value < amount)
            revert NotEnoughEther();

        _;
        if (msg.value > amount)
            payable(msg.sender).transfer(msg.value - amount);
    }

    function forceOwnerChange(address newOwner)
        public
        payable
        costs(200 ether)
    {
        owner = newOwner;
        // just some example condition
        if (uint160(owner) & 0 == 1)
            // This did not refund for Solidity
            // before version 0.4.0.
            return;
        // refund overpaid fees
    }
}

```

--------------------------------

### Solidity: Dangling reference from tuple assignment with complex expressions

Source: https://docs.soliditylang.org/en/v0.8.30/types

Illustrates dangling references in Solidity using tuple assignments with complex expressions. Operations like `s.push()` on the left-hand side, combined with function calls that modify arrays on the right-hand side, can create dangling references and unexpected writes.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.0 <0.9.0;

contract C {
    uint[] s;
    uint[] t;
    constructor() {
        // Push some initial values to the storage arrays.
        s.push(0x07);
        t.push(0x03);
    }

    function g() internal returns (uint[] storage) {
        s.pop();
        return t;
    }

    function f() public returns (uint[] memory) {
        // The following will first evaluate ``s.push()`` to a reference to a new element
        // at index 1. Afterwards, the call to ``g`` pops this new element, resulting in
        // the left-most tuple element to become a dangling reference. The assignment still
        // takes place and will write outside the data area of ``s``.
        (s.push(), g()[0]) = (0x42, 0x17);
        // A subsequent push to ``s`` will reveal the value written by the previous
        // statement, i.e. the last element of ``s`` at the end of this function will have
        // the value ``0x42``.
        s.push();
        return s;
    }
}

```

--------------------------------

### Solidity: tx.origin and msg.sender type

Source: https://docs.soliditylang.org/en/v0.8.30/080-breaking-changes

The global variables `tx.origin` and `msg.sender` now have the type `address` instead of `address payable`. Explicitly convert to `address payable` using `payable()`.

```Solidity
tx.origin
```

```Solidity
msg.sender
```

```Solidity
payable(tx.origin)
```

```Solidity
payable(msg.sender)
```

--------------------------------

### Solidity Invalid Instruction (invalid)

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Terminates execution with an invalid instruction error. This is typically used for handling exceptional cases or unimplemented features.

```Solidity
invalid();
```

--------------------------------

### Solidity Withdrawal Pattern for Secure Fund Sending

Source: https://docs.soliditylang.org/en/v0.8.30/common-patterns

Implements the withdrawal pattern to securely send Ether from a contract. It stores pending withdrawals in a mapping and allows users to withdraw their funds safely, preventing reentrancy issues that can arise from direct transfers.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.4;

contract WithdrawalContract {
    address public richest;
    uint public mostSent;

    mapping(address => uint) pendingWithdrawals;

    /// The amount of Ether sent was not higher than
    /// the currently highest amount.
    error NotEnoughEther();

    constructor() payable {
        richest = msg.sender;
        mostSent = msg.value;
    }

    function becomeRichest() public payable {
        if (msg.value <= mostSent) revert NotEnoughEther();
        pendingWithdrawals[richest] += msg.value;
        richest = msg.sender;
        mostSent = msg.value;
    }

    function withdraw() public {
        uint amount = pendingWithdrawals[msg.sender];
        // Remember to zero the pending refund before
        // sending to prevent reentrancy attacks
        pendingWithdrawals[msg.sender] = 0;
        payable(msg.sender).transfer(amount);
    }
}

```

--------------------------------

### Solidity: ECDSA ecrecover

Source: https://docs.soliditylang.org/en/v0.8.30/units-and-global-variables

Recovers the address associated with a public key from an elliptic curve signature (hash, v, r, s) or returns zero on error. Note potential issues with signature malleability on private blockchains.

```Solidity
ecrecover(bytes32 hash, uint8 v, bytes32 r, bytes32 s) returns (address)
```

--------------------------------

### Solidity: Escape sequences in string literals

Source: https://docs.soliditylang.org/en/v0.8.30/080-breaking-changes

Support for the escape sequences `\b`, `\f`, and `\v` in string literals has been removed. Use hexadecimal escapes like `\x08`, `\x0c`, and `\x0b` instead.

```Solidity
"Hello\bWorld"
```

```Solidity
"Hello\x08World"
```

--------------------------------

### Solidity Unicode String Literal

Source: https://docs.soliditylang.org/en/v0.8.30/types

Shows how to declare a string literal in Solidity that includes Unicode characters, such as emojis. These literals are prefixed with the 'unicode' keyword.

```Solidity
string memory a = unicode"Hello 😃";
```

--------------------------------

### Solidity Array Assignment Behavior (Memory vs. Storage)

Source: https://docs.soliditylang.org/en/v0.8.30/control-structures

Illustrates the difference in assignment behavior for arrays when passed to functions. Passing an array to a function with a 'memory' data location creates an independent copy, while passing with a 'storage' data location allows modification of the original array.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.22 <0.9.0;

contract C {
    uint[20] x;

    function f() public {
        g(x);
        h(x);
    }

    function g(uint[20] memory y) internal pure {
        y[2] = 3;
    }

    function h(uint[20] storage y) internal {
        y[3] = 4;
    }
}

```

--------------------------------

### Solidity Direct Transfer for Fund Sending (Insecure)

Source: https://docs.soliditylang.org/en/v0.8.30/common-patterns

Illustrates a less secure method of sending Ether directly using `transfer`. This pattern can lead to contracts being trapped in an unusable state if the recipient contract's fallback function fails, due to gas limitations or explicit reverts.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.4;

contract SendContract {
    address payable public richest;
    uint public mostSent;

    /// The amount of Ether sent was not higher than
    /// the currently highest amount.
    error NotEnoughEther();

    constructor() payable {
        richest = payable(msg.sender);
        mostSent = msg.value;
    }

    function becomeRichest() public payable {
        if (msg.value <= mostSent) revert NotEnoughEther();
        // This line can cause problems (explained below).
        richest.transfer(msg.value);
        richest = payable(msg.sender);
        mostSent = msg.value;
    }
}

```

--------------------------------

### Solidity: Update function call syntax

Source: https://docs.soliditylang.org/en/v0.8.30/070-breaking-changes

Updates the syntax for function calls involving value and gas transfers in Solidity. It changes the way value and gas are passed to external function calls and constructor calls.

```solidity
Change `x.f.value(...)()` to `x.f{value: ...}()`. Similarly `(new C).value(...)()` to `new C{value: ...}()` and `x.f.gas(...).value(...)()` to `x.f{gas: ..., value: ...}()`.
```

--------------------------------

### Solidity: Contract and uint type conversion

Source: https://docs.soliditylang.org/en/v0.8.30/080-breaking-changes

Converting from `uint` to `Contract` types is restricted due to changes in type-category and width. Use an intermediate conversion to `address`.

```Solidity
Contract(uint)
```

```Solidity
Contract(address(uint160(uint)))
```

--------------------------------

### Solidity Getter for Complex Struct Members

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Demonstrates how Solidity generates getter functions for public state variables that are structs containing primitive types and byte arrays. Mappings and dynamic arrays within structs are omitted from auto-generated getters due to complexity.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

contract Complex {
    struct Data {
        uint a;
        bytes3 b;
        mapping(uint => uint) map;
        uint[3] c;
        uint[] d;
        bytes e;
    }
    mapping(uint => mapping(bool => Data[])) public data;
}
```

```solidity
function data(uint arg1, bool arg2, uint arg3)
    public
    returns (uint a, bytes3 b, bytes memory e)
{
    a = data[arg1][arg2][arg3].a;
    b = data[arg1][arg2][arg3].b;
    e = data[arg1][arg2][arg3].e;
}
```

--------------------------------

### Solidity Linearization Error - Diamond Problem

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Demonstrates a contract inheritance structure that violates Solidity's C3 Linearization rules, leading to a 'Linearization of inheritance graph impossible' error. This occurs when a contract inherits from two contracts that both inherit from a common base contract, and the inheritance order creates a conflict.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

contract X {}
contract A is X {}
// This will not compile
contract C is A, X {}
```

--------------------------------

### Solidity Transaction Sender (origin)

Source: https://docs.soliditylang.org/en/v0.8.30/yul

Returns the address of the original sender of the current transaction. This is the address that initiated the transaction externally.

```Solidity
address sender = origin();
```

--------------------------------

### Solidity: No Explicit Override Needed for Common Base

Source: https://docs.soliditylang.org/en/v0.8.30/contracts

Shows a scenario where explicit override is not required. This occurs when a function is inherited from multiple bases that share a common ancestor defining the function, or when there's a unique overriding function in a common base.

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

contract A { function f() public pure{} }
contract B is A {}
contract C is A {}
// No explicit override required
contract D is B, C {}

```

--------------------------------

### Secure Withdraw Function using Checks-Effects-Interactions in Solidity

Source: https://docs.soliditylang.org/en/v0.8.30/security-considerations

This Solidity code snippet demonstrates how to prevent reentrancy by using the Checks-Effects-Interactions pattern. The contract updates its state before transferring Ether, preventing attackers from re-entering the function.  Requires Solidity version >=0.6.0 and <0.9.0.

```Solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

contract Fund {
    /// @dev Mapping of ether shares of the contract.
    mapping(address => uint) shares;
    /// Withdraw your share.
    function withdraw() public {
        uint share = shares[msg.sender];
        shares[msg.sender] = 0;
        payable(msg.sender).transfer(share);
    }
}

```

--------------------------------

### Solidity `byte` to `bytes1` Type Conversion

Source: https://docs.soliditylang.org/en/v0.8.30/080-breaking-changes

Illustrates the change in Solidity where the `byte` type should be replaced with `bytes1` for explicit type safety.

```Solidity
bytes1
```

--------------------------------

### Solidity Code Update: Function Signature for Receive/Fallback

Source: https://docs.soliditylang.org/en/v0.8.30/060-breaking-changes

Explains the modification of function signatures for handling incoming Ether. The old `function () external [payable]` syntax should be replaced with `receive()` or `fallback()`.

```solidity
// Old syntax
// function () external payable { ... }

// New syntax (prefer receive if possible)
receive() external payable { ... }
// or
fallback() external payable { ... }
```