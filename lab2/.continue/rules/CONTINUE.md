# IBM i Modernization Labs 101 - Project Guide

## Project Overview

This repository contains **IBM i Modernization Labs 101**, a comprehensive learning program designed to teach developers how to modernize legacy IBM i (AS/400) applications using **IBM Bob AI assistant**. The labs use a sample green-screen order management application called **SAMCO** written in legacy RPG, CL, COBOL, and DDS.

### Key Technologies
- **IBM Bob**: AI-powered development assistant with specialized modes for IBM i modernization
- **SAMCO Application**: A 20+ year old legacy order management system with green screen interface
- **RPG (COBOL-like)**: Legacy RPG fixed-format code to modern free-format RPG conversion
- **IBM i Platform**: Db2 for i, DDS (Data Description Specifications), CL programs
- **React + Carbon Design System**: Modern web UI modernization examples
- **MCP (Model Context Protocol)**: External tool integrations for IBM i systems
- **Ansible**: Infrastructure automation for IBM i system management

### Architecture
The project follows a learning lab structure with:
- **SAMCO Application**: Legacy IBM i application with RPG/CL/DDS source code
- **Modernization Labs**: Step-by-step guides (6 labs) for different modernization scenarios
- **Bob Configuration**: MCP servers, custom modes, and tool definitions for IBM i development
- **Documentation**: Lab guides, best practices, and architecture diagrams

---

## Getting Started

### Prerequisites
- IBM Bob with Code for IBM i extension
- Basic understanding of RPG/IBM i concepts
- Git installed
- Optional: IBM i system (7.3+) for building SAMCO

### Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/bmarolleau/IBM-i-Application-Modernization-with-Bob
   cd IBM-i-Application-Modernization-with-Bob
   ```

2. Open in IBM Bob or VS Code with Code for IBM i extension

3. Configure Bob with IBM i MCP servers (already configured in `.bob/mcp.json`)

### Basic Usage
1. Run `/init` command in Bob to analyze the project structure
2. Select an appropriate mode (IBM i Developer, IBM i Agent, etc.)
3. Follow lab prompts with specific file references like:
   ```
   @SAMCO/QRPGLESRC/ART200-Work_with_article.PGM.SQLRPGLE
   Explain what the s01lod subroutine does.
   ```

### Building SAMCO (Optional)
To build and test the green screen application on IBM i:
```bash
cd SAMCO
export lib1=SAMCO
system "addlible SAMCO"
/QOpenSys/pkgs/bin/makei build
```

---

## Project Structure

```
├── SAMCO/                    # Legacy IBM i application
│   ├── QRPGLESRC/           # Modern free-format RPG source
│   ├── QRPGSRC/             # Legacy fixed-format RPG source
│   ├── QCLSRC/              # CL (Control Language) programs
│   ├── QSQLSRC/             # SQL procedures, triggers, views
│   ├── QDDSSRC/             # DDS source (files, displays, etc.)
│   ├── QPROTOSRC/           # RPG prototypes/includes
│   ├── common/              # Shared files and includes
│   ├── functionsVAT/        # VAT calculation functions
│   ├── globalization/       # Internationalization files
│   ├── iproj.json           # Project metadata for Tobi build
│   └── Rules.mk             # Makefile for build system
├── .bob/                     # Bob AI configuration
│   ├── custom_modes.yaml    # Custom agent mode definitions
│   ├── mcp.json             # MCP server configurations
│   ├── tools/               # YAML tool definitions
│   └── rules-ibmi-mcp-tool-builder/  # Tool creation guidelines
├── pics/                     # Screenshots and diagrams
├── lab*.md                   # Modernization lab guides
├── bob-concepts-and-best-practices.md  # Bob usage guide
└── README.md                 # Project overview
```

### Key Files

| File | Purpose |
|------|---------|
| `SAMCO/iproj.json` | Project configuration for Tobi build system |
| `SAMCO/QRPGLESRC/ART200*.PGM.*` | Article management program (main example) |
| `SAMCO/QRPGLESRC/ORD200*.PGM.*` | Order management program |
| `.bob/custom_modes.yaml` | Custom AI agent mode definitions |
| `.bob/mcp.json` | Model Context Protocol server configuration |
| `bob-concepts-and-best-practices.md` | Best practices for using Bob |

---

## Development Workflow

### Using IBM Bob Effectively

1. **Choose the Right Mode**
   - `IBM i Developer`: For code understanding and modernization
   - `IBM i Agent`: For system exploration and analysis
   - `IBM i MCP Tool Builder`: For creating custom tools

2. **Use File References**
   Always include file references with @ prefix:
   ```
   @SAMCO/QRPGLESRC/ART200-Work_with_article.PGM.SQLRPGLE
   Explain the panel-step pattern used here.
   ```

3. **Incremental Modernization**
   - Start with understanding (Lab 0)
   - Convert code format (Lab 1)
   - Replace RLA with SQL (Lab 3)
   - Build modern UI (Lab 2)

4. **Best Practices**
   - Run `/init` at project start
   - Use Agentic Chat for multi-file tasks
   - Use Inline Assistant for quick edits
   - Break complex tasks into steps

### Build System
- **Tobi (makei)**: Project build tool for IBM i
- **Build command**: `/QOpenSys/pkgs/bin/makei build`
- **Clean**: `/QOpenSys/pkgs/bin/makei clean`

---

## Key Concepts

### IBM i Modernization Patterns

1. **Fixed-to-Free RPG Conversion**
   - Convert legacy fixed-format RPG to free-format
   - Replace magic numbers with named constants
   - Use procedures instead of subroutines

2. **RLA to SQL Conversion**
   - Replace Record Level Access with SQL
   - Use JOINs for related data
   - Benefits: better performance, easier maintenance

3. **Green Screen to Web UI**
   - Convert 5250 panel interfaces to React
   - Use Carbon Design System for consistent UI
   - Maintain business logic while modernizing presentation

### SAMCO Application Structure

1. **Panel-Step Pattern**: State machine pattern for interactive programs
   - Steps: prepare → load → display → key → check → act
   - Used in all interactive programs

2. **Soft Deletes**: Instead of deleting records, mark with indicator
   - `ARDEL = 'X'` marks articles as deleted
   - Preserves historical data

3. **VAT Calculation**: Business rule for tax computation
   - Formula: `VAT = (net × rate) / 100`
   - Configured through article families

4. **Order Management**: Complete order lifecycle
   - Header (ORDER) + Lines (DETORD)
   - Three states: created, delivered, closed
   - Atomic transactions with locking

---

## Common Tasks

### Understanding Legacy Code
1. Open the file in Bob
2. Use prompts like:
   ```
   @SAMCO/QRPGLESRC/ART200-Work_with_article.PGM.SQLRPGLE
   Explain the s01lod subroutine (lines 102-118).
   ```

### Converting RPG Code
1. Identify the subroutine to convert
2. Use Bob's conversion prompts
3. Test the converted code
4. Update references

### Building Modern UI
1. Understand the green screen layout
2. Create React components with Carbon Design System
3. Connect to backend services
4. Test the web interface

### Creating MCP Tools
1. Define SQL queries in YAML format
2. Follow security requirements
3. Test with Bob's tool builder mode
4. Integrate into your workflow

---

## Troubleshooting

### Common Issues

**Bob Not Responding**
- Check file references are correct
- Try rephrasing the question
- Ensure proper mode selection

**Build Failures**
- Verify Tobi is installed on IBM i
- Check library list configuration
- Ensure source files are in correct library

**npm Install Issues**
```bash
cd article-management-web
rm -rf node_modules package-lock.json
npm install
```

**SQL Syntax Errors**
- Check working examples in ART400 files
- Use Bob to explain specific errors
- Verify table/column names match

### Debugging Tips
1. Use Bob's explain capabilities
2. Check file references with @ prefix
3. Use incremental conversion approach
4. Test converted code before proceeding

---

## References

- [IBM Bob Documentation](https://bob.ibm.com/docs/)
- [Carbon Design System](https://carbondesignsystem.com/)
- [Tobi Build System](https://ibm.github.io/ibmi-tobi/#/)
- [Code for IBM i Extension](https://marketplace.visualstudio.com/items?itemName=HalcyonTechLtd.code-for-ibmi)
- [RPG Cafe](https://www.rpgpgm.com/)

---

*This project guide was automatically generated to help developers understand and work with the IBM i Modernization Labs codebase. For detailed lab instructions, see the individual lab*.md files.*