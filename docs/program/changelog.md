# Changelog

All notable changes to Partner Market Launchpad content are documented here so partners and facilitators always know what has been updated.

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
