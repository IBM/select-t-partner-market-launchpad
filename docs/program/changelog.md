# Changelog

All notable changes to Partner Market Launchpad content are documented here so partners and facilitators always know what has been updated.

---

## [1.2.0] — 2026-05-13

### Added
- New HR Agent use case for Track 01 Lab 101 (`docs/tracks/track-01/labs/lab-101/hr/`)
- Wealth Manager use case for Track 01 Lab 201 Financial Services domain
- Self-service KYC use case for Track 01 Lab 301 Financial Services domain
- Complete Track 03 Maximo documentation structure with all labs (101-401)
- "Coming Soon" placeholders for Track 02 and Track 04

### Changed
- **Track 01 index page** (`docs/tracks/track-01/index.md`):
    - Updated products table with numbered icons and improved formatting
    - Changed "Theory sessions" to "Overview sessions"
    - Restructured "Before You Begin" section with warning callout
    - Added comprehensive lab descriptions with learning objectives for all labs (101-401)
    - Improved lab cards with detailed use case descriptions
    - Enhanced navigation structure with domain-specific lab guides
- **Navigation structure** (`mkdocs.yml`):
    - Reorganized Track 01 labs to remove redundant overview pages
    - Added HR Agent use case to Lab 101
    - Restructured Lab 201, 301, and 401 with domain-specific use cases
    - Removed "Domains" overview page from Track 01
    - Added complete Track 03 Maximo navigation with theory and labs
    - Updated Track 02 and Track 04 to show "Coming Soon" pages
- **Facilitator lab environment setup** (`docs/facilitator/lab-environment-setup.md`):
    - Updated Track 02 and Track 04 links to show "Coming Soon" status
    - Removed broken links for tracks not yet available

### Removed
- Track 01 domains overview page (`docs/tracks/track-01/domains/overview.md`)
- Multiple redundant lab overview pages across Track 01 labs
- Placeholder Track 02 and Track 04 theory and lab files (moved to "Coming Soon")
- Lab 101 prerequisites page from Track 01

---

## [1.1.0] — 2026-04-30

### Added
- New IBMid creation guide for facilitators (`docs/facilitator/create-ibm-id.md`)
- Comprehensive Track 01 lab environment setup documentation with TechZone provisioning instructions
- New image assets for Track 01:
    - Customer service use case images (34 screenshots)
    - Insurance use case images
    - Vehicle maintenance use case images
    - Lab setup screenshots (TechZone, IBMid creation, watsonx Orchestrate settings)
- Operating system compatibility note for lab commands (MacOS/Linux focus)

### Changed
- **Audience documentation restructure** (`docs/program/audience.md`):
    - Reduced from three to two primary audience groups
    - Renamed "Select-T Partners" section to "Partner-Facing Stakeholders"
    - Renamed "Business Technical Leaders (BTLs)" section to "Client-Facing Stakeholders"
    - Removed "Select-T Clients" as separate audience (now represented as context)
    - Updated role descriptions to reflect IBM stakeholder focus (BTSS, BSS, PTS, TPS, ATL)
    - Clarified that program enables IBM stakeholders who work with partners and clients
- **Homepage updates** (`docs/index.md`):
    - Updated program description to reference "select-t growth partners"
    - Updated audience table with new terminology
- **Lab documentation updates**:
    - Multiple Track 01, 02, 03, and 04 lab files updated with new terminology
    - Troubleshooting pages updated across all tracks
- **Lab environment setup timing**: Reduced from 24 hours to 12 hours before session
- **Track 01 lab environment setup**: Complete rewrite with TechZone-based provisioning
    - Replaced IBM Cloud CLI provisioning with TechZone bundle approach
    - Updated environment requirements table (removed API keys, added TechZone details)
    - Added detailed TechZone reservation and validation steps
    - Included watsonx Orchestrate configuration instructions
- **Track 01 index**: Updated "Before You Begin" section with IBMid creation requirement
- **Navigation structure** (`mkdocs.yml`):
    - Renamed use cases with descriptive titles:
        - Retail: "AI Powered customer service"
        - Automobile: "Vehicle Maintenance"
        - Insurance: "Insurance broker assistant"
    - Removed Lab 101 prerequisites page
    - Commented out secondary use cases for Automobile and Insurance domains

---

## [1.0.0] — 2026-04-29

### Added
- Initial release of Partner Market Launchpad program framework
- Complete program documentation:
    - Program overview with goals, structure, and lab progression framework
    - Intended audience guide covering Select-T Partners, BTLs, and Select-T Clients
    - Mode of conduct guidelines
    - Partner pipeline visualization and documentation
- Four complete track structures (Track 01–04):
    - Each track includes theory modules (What & Why, Product Overview, Use Cases & Personas)
    - Progressive lab structure: Lab 101 (Basics) → Lab 201 (Fundamentals) → Lab 301 (Intermediate) → Lab 401 (Advanced)
    - Each lab includes: Overview, Prerequisites, Steps, Validation, and Recap sections
    - Troubleshooting guides for each track
- Comprehensive facilitator guide:
    - Running the program guidelines
    - Session planning framework
    - Lab environment setup instructions
    - FAQ handling strategies
- Resources section:
    - Further reading materials
    - Glossary of terms
    - Support and help documentation
- MkDocs site configuration with Carbon Design System theming
- Custom Carbon CSS styling
- Navigation structure with tabs and sections

---

!!! note "Content Update Policy"
    When a lab or theory module is updated, the version number and change summary will be logged here. Always check this page if you are returning to a track you have run before.
