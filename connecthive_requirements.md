# ConnectHive --- Product Requirements Document

**Document status:** Draft --- consolidated requirements\
**Version:** 1.0\
**Last updated:** 28 October 2026

## 1. Product Overview

ConnectHive is a multi-villa management platform. Villa vendors, villa
owners, and the superadmin manage villa information through
role-specific dashboards. Guests access a villa-specific public
information page by scanning a QR code. Guests do not need to create an
account or log in.

The platform should use one shared application while keeping each
villa's content, design configuration, QR destination, and analytics
associated with the correct villa.

## 2. Goals

-   Provide each villa with a convenient, mobile-friendly guest
    information page.
-   Let authorized villa owners maintain the information shown to
    guests.
-   Let villa vendors manage multiple villas and review villa-level
    performance.
-   Let the superadmin manage users, assignments, villa content, and
    platform-wide analytics.
-   Support per-villa themes, layouts, and configurable page sections.
-   Measure guest engagement with useful, clearly labelled analytics.

## 3. User Roles and Access

### 3.1 Superadmin

The superadmin owns and administers the ConnectHive platform.

Requirements: - Manage villa vendor accounts. - Manage villa owner
accounts. - Create and manage villa records. - Assign a villa vendor and
villa owner to each villa. - View and update the guest-facing content
and configuration for any villa. - View analytics for individual villas
and aggregate platform performance. - Manage platform-level settings and
access. - Have an audit trail for important administrative actions,
especially content edits and assignment changes.

### 3.2 Villa Vendor

A villa vendor manages multiple villas.

Requirements: - View a list of villas associated with the vendor. - View
villa details, assigned owners, QR access, and publication status. -
Open a villa to manage or review its information, subject to the
permission model defined for the product. - View analytics for each
villa assigned to the vendor. - View aggregated analytics across the
vendor's villas. - View which villa owner is assigned to each villa.

Access boundary: - A vendor must only access villas associated with
their own vendor account. - A vendor must not access another vendor's
villas or data.

### 3.3 Villa Owner

A villa owner owns/manages one villa and belongs to a villa vendor.

Requirements: - Access the dashboard for their assigned villa. - Update
the information displayed on the guest page. - Manage villa name and
description. - Manage villa gallery and media. - Manage Wi-Fi details
intended for guests. - Upload and maintain a house guide PDF and house
rules. - Manage the food menu. - Manage experiences offered by the
villa. - Manage nearby places and map-related information. - Manage
social media links. - Manage review links or supported review content. -
Configure guest help/contact options. - Customize supported theme and
layout settings. - Preview changes before publishing them. - Publish
updates to the guest page. - View analytics for their own villa. - View
or download the villa's QR code.

Access boundary: - A villa owner must only edit and view private
management information for their assigned villa. - The backend must
enforce permissions; hiding another villa in the frontend alone is
insufficient.

### 3.4 Guest

Guests use the public guest experience without logging in.

Requirements: - Scan a villa-specific QR code. - Open the correct
villa's public information page. - Browse published villa information on
a mobile browser. - Access only information intended to be public or
available to guests. - Use relevant contact, map, social, menu, and
experience links.

Guests do not need an account, password, or authenticated session to
view the public page.

## 4. Guest Landing Page Requirements

Each villa has its own public page, associated with its own QR code and
saved content/configuration.

### 4.1 Villa Details

-   Display the villa name.
-   Display the villa description.

### 4.2 Villa Gallery

-   Display photos of the villa, rooms, facilities, and other approved
    property images.
-   Associate gallery media with the correct villa.

### 4.3 Wi-Fi

-   Display the Wi-Fi network name and password when configured by the
    villa owner.
-   Present the information in a guest-friendly format.
-   Only expose Wi-Fi credentials intentionally designated for guest
    access.

### 4.4 House Guide and House Rules

-   Allow an owner or authorized administrator to upload a house guide
    PDF.
-   Convert the PDF's useful content into readable UI sections/pages,
    rather than relying only on an embedded PDF viewer.
-   Display house rules.
-   Preserve a way to access the original PDF where appropriate.
-   Handle extraction failures or scanned PDFs with an appropriate
    fallback or manual-editing path.

### 4.5 Food Menu

-   Display the villa's food menu.
-   Support menu items and relevant details such as descriptions and
    prices where provided.
-   Allow the owner to update menu content.

### 4.6 Experiences We Offer

-   Provide a dedicated page or section for experiences offered by the
    villa.
-   Display experience details and relevant images or links where
    available.
-   Allow owners to manage the experiences shown.

### 4.7 Explore Around You

-   Provide a map and nearby places to visit.
-   Support places such as attractions, restaurants, and points of
    interest.
-   Associate the starting location and curated nearby places with the
    villa.
-   Do not require live guest location access when villa-based nearby
    recommendations are sufficient.
-   Request location permission only if a feature genuinely needs the
    guest's current location.

### 4.8 Socials

-   Display the villa's configured social media handles or profile
    links.
-   Only display links that have been provided and enabled.

### 4.9 Reviews

-   Support links to external review platforms and/or displaying reviews
    collected by ConnectHive, depending on the selected product scope.
-   Clearly distinguish a review link click from a review actually
    submitted.
-   The exact review model is still to be decided.

### 4.10 Need Help

-   Provide a clear way for guests to contact the villa's designated
    contact or support person.
-   Potential channels include phone, WhatsApp, or a contact form; the
    final selection is still to be decided.
-   Contact details must be configurable per villa.

## 5. Per-Villa Themes, Layouts, and Content

ConnectHive should support a configuration-driven guest page. A shared
frontend renders the page using the content and configuration for the
requested villa.

### 5.1 Villa-Specific Data

Each villa's data must remain separate and may include: - Name and
description. - Gallery and other media. - Wi-Fi details. - House guide
content and rules. - Food menu. - Experiences. - Location and nearby
places. - Social links. - Review configuration. - Help/contact
information.

### 5.2 Theme Configuration

Supported customization may include: - Primary and secondary colors. -
Fonts and typography choices. - Light or dark theme. - Button
appearance. - Card styles, spacing, and visual treatments. - Hero/header
presentation.

### 5.3 Layout Configuration

Supported customization may include: - Choosing from predefined page
templates. - Selecting supported layouts for page sections. - Reordering
sections. - Showing or hiding optional sections. - Previewing the page
before publishing.

### 5.4 Customization Guardrails

-   Prefer predefined themes and layout templates for the initial
    release.
-   Do not allow arbitrary HTML or JavaScript uploads as a customization
    mechanism.
-   Keep content, theme configuration, and layout configuration
    separate.
-   A design change must not accidentally alter villa content.
-   A content change must not unexpectedly reset the design.
-   Customization controls should be responsive and usable on mobile and
    desktop.

## 6. QR Code and Public Page Flow

Requirements: 1. Each villa has a unique, stable public URL or slug. 2.
Each villa has a QR code that points to its public page. 3. Scanning the
QR code resolves the correct villa. 4. The public page loads that
villa's published content, theme, and layout configuration. 5. Guests
can access the public page without authentication. 6. Owners and
authorized administrators can view or download the QR code. 7. Editing
the villa's content should not require generating a new QR code. 8. The
system must not expose dashboards, private owner information, or vendor
data through the public route. 9. The page should work well on mobile
devices and common browsers. 10. The system should define behavior for
unpublished, disabled, or unavailable villas.

## 7. Dashboards

### 7.1 Villa Owner Dashboard

-   Overview of the owner's assigned villa.
-   Entry points to edit all guest-page content areas.
-   Theme and layout customization.
-   Guest-page preview.
-   Draft and publish controls.
-   QR code viewing/downloading.
-   Villa analytics.

### 7.2 Villa Vendor Dashboard

-   List of the vendor's villas.
-   Villa name and publication status.
-   Assigned owner information.
-   Access to an individual villa's management or review view according
    to permissions.
-   Analytics for each villa.
-   Aggregated analytics across the vendor's villas.

### 7.3 Superadmin Dashboard

-   Manage vendor accounts.
-   Manage owner accounts.
-   Create and manage villas.
-   Assign vendors and owners to villas.
-   View and update any villa's guest-page data and configuration.
-   View individual villa analytics.
-   View platform-wide analytics.
-   Review important administrative changes through an audit log.

## 8. Analytics Requirements

The final analytics scope has not yet been decided. The following is a
recommended starting point, not a finalized commitment.

### 8.1 Recommended MVP Metrics

-   QR scan activity.
-   Guest-page views.
-   Unique visitors, where reliably measurable.
-   Views or interactions by section, such as house guide, Wi-Fi, menu,
    and experiences.
-   Clicks on help/contact actions.
-   Map interactions and external social/review link clicks where
    instrumented.
-   Trends over a selected time period.

### 8.2 Vendor Analytics

-   Compare engagement across villas belonging to the vendor.
-   View analytics for an individual villa.
-   Aggregate villa metrics without exposing another vendor's data.

### 8.3 Superadmin Analytics

-   View aggregate platform activity.
-   Drill down into individual villas.
-   View metrics across vendors where authorized.

### 8.4 Analytics Definitions and Privacy

-   A QR scan, page view, and unique visitor are different metrics and
    must be labelled accordingly.
-   A click on a review link does not prove a review was submitted.
-   A help button click does not necessarily mean a request was
    resolved.
-   Define session and unique-visitor counting rules before
    implementation.
-   Collect only the analytics data needed for product purposes and
    document applicable privacy expectations.
-   Analytics access must follow role and villa boundaries.

## 9. Suggested Data Model

The following is a suggested starting structure. The final schema may
combine or split entities as implementation details become clearer.

-   `villa_vendors`: vendor accounts.
-   `villa_owners`: owner accounts and vendor relationship.
-   `villas`: villa identity, public slug, vendor assignment, owner
    assignment, location, and publication status.
-   `villa_content`: structured guest-facing information, if not stored
    directly on the villa record.
-   `villa_media`: gallery and other media files.
-   `villa_page_configs`: theme and layout settings.
-   `villa_sections`: optional per-section configuration and ordering.
-   `villa_guide_documents`: house guide PDF metadata and
    extracted/edited content, if required.
-   `villa_menu_items`: food menu entries, if a structured menu is
    needed.
-   `villa_experiences`: experiences offered by a villa.
-   `villa_places`: curated nearby places.
-   `villa_social_links`: social media links.
-   `villa_analytics_events` or an analytics provider: tracked page and
    section events.
-   `admin_audit_logs`: important administrative actions.

Data must be associated with the appropriate villa, and server-side
authorization must prevent cross-villa access.

## 10. Security and Access Control

-   Enforce role-based permissions in the backend.
-   Enforce vendor-to-villa and owner-to-villa relationships on every
    relevant API operation.
-   Do not rely only on frontend filtering to protect data.
-   Keep management dashboards behind authentication.
-   Keep public guest routes limited to approved public/guest-facing
    fields.
-   Protect private account data and administrative functionality.
-   Validate uploaded files, including PDFs and images.
-   Avoid executing arbitrary user-provided HTML or JavaScript.
-   Maintain audit records for important administrative changes.
-   Define a safe policy for unpublished or disabled villas.

## 11. Non-Functional Requirements

-   Mobile-first guest experience.
-   Responsive owner, vendor, and superadmin dashboards.
-   Reasonable page-load performance on mobile networks.
-   Accessible text, controls, and navigation.
-   Clear error states for missing content, invalid villa URLs, and
    failed document processing.
-   Consistent behavior across supported browsers.
-   Reliable media and PDF storage.
-   Scalable shared application architecture that can serve many villas.
-   Data isolation and authorization tests.
-   Observability for errors in QR resolution, page rendering, uploads,
    and analytics collection.

## 12. Suggested MVP Scope

Recommended first release: 1. Authentication and role-based dashboards
for superadmin, villa vendors, and villa owners. 2. Villa creation and
owner/vendor assignment. 3. Public villa page with a unique QR code. 4.
Villa name, description, gallery, Wi-Fi, house guide/rules, menu,
experiences, nearby places, socials, reviews links, and help/contact
details. 5. Per-villa content management. 6. A small set of predefined
themes and layouts. 7. Section visibility and ordering. 8. Preview and
publish workflow. 9. Basic QR/page/section engagement analytics. 10.
Server-side access control and audit logging for administrative actions.

Advanced drag-and-drop page building, detailed reporting, in-platform
review collection, and automated PDF extraction can be considered after
the initial release requirements are validated.

## 13. Open Decisions

The following items are not yet finalized: - Exact dashboard analytics
and metric definitions. - Whether vendors can edit villa content or only
view/manage it. - Whether the theme editor offers predefined templates
only or more advanced layout controls. - Whether PDF-to-UI conversion is
automated, manually editable, or both. - Whether reviews are external
links, native reviews, or both. - Which contact channels are supported
under "Need Help." - Whether menus and experiences need prices,
categories, availability, or inquiry/booking actions. - How nearby
places are sourced and maintained. - How unique visitors and sessions
are measured. - Whether owners can save drafts and schedule
publication. - What happens to a villa's public page and QR destination
when a villa is disabled or reassigned.

## 14. Core Product Principles

-   One shared platform, not a separately deployed website for every
    villa.
-   Each villa has separate content and page configuration.
-   Each villa has its own QR code and public page.
-   Guests do not need to log in.
-   Villa owners manage one assigned villa.
-   Villa vendors manage multiple villas within their scope.
-   Superadmin has platform-wide administrative access.
-   Public guest information is separated from private management data.
-   Analytics and management access follow the same role and villa
    boundaries.
-   Unfinalized decisions remain explicitly marked as open rather than
    treated as implemented requirements.
