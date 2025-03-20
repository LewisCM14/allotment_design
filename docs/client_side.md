## Client Side Requirements

The aim with the client side of the application, like the database and server side layers is to support the applications overall modular design by not being tightly coupled to the other architecture layers, whilst still enforcing data consistency and integrity. 

All while delivering a progressive web application experience to many concurrent end users by supporting offline capabilities in an accessible mobile first application with a simple yet effective user interface.

<u>**Requirements:**</u>

- Please refer to the [High Level Requirements](overview.md).

- Must integrate with a RESTful API written using the FastAPI framework.
- Must be able to handle JWTs for user authentication provided from the sever side via fastapi.security and Authlib.
- Must be able to facilitate the creation of a Progressive Web App.
    - The developer is familiar with JavaScript/TypeScript based frameworks like React and Vue but open to other technologies.
    - The developer is able to produce their own custom components or make use of component libraries like Mui, Tailwind and Bootstrap. But any library used must be free for commercial use.
- Must be able to provide type safety and complete form validation for data consistency and integrity across the application.
- Must be able to provide offline capabilities and caching in order to accommodate users with allotments in low signal areas.
- The only required global state is authentication state, everything else can be handled with simple UI state.

!!! info
    There is currently no suspected need for heavy data synchronization between the front and backend.

!!! tip "Future Improvement"
    Whilst the need for real time updates via push notifications is beyond the scope of a minimal viable product. The ability to deliver upon this is desired long term in order to create a feature rich application.

<u>**Testing Considerations**:</u>

- Integration tests against the API are to be prioritized as these provide the most benefit in ensuring the modular architecture pieces together. 
- In the instance custom components are created the testing of these should be prioritized over components built using the supporting tech stack.

!!! info
    Testing the happy pathway is to be prioritized and deemed sufficient unless a bug is discovered that steers the application away from intended functionality. In this instance a test confirming the bug is no longer present is to be written first before a resolution is implemented, following Test Driven Development (TDD) principles and allowing for an automated check that the ensures the application does not regress in the future.

---

## Interfaces Required

_High level interface functionality accompanied by low fidelity designs._

![Wireframes](wireframe.svg){ loading=lazy }

### User Account Interfaces

<u>_**High Priority**_</u>

=== "User Registration Interface"
    - Ability for users to register an account within the application using an email address and password.
        - Users must also provide a first name and country code.
        - Emails must be unique and singing up with an existing one should trigger the password reset flow.

=== "User Login Interface"
    - Ability for users to sign into the application via email and password
        - Ability for users to request a password reset.
        - Ability for users to trigger the registration window if they do not have an account.

=== "User Owned Grow Guide Interface"
    - A interface to list a users currently owned grow guides with a flow for activating/deactivating a guide. As well as a flow for deleting a guide that will also require an "are you sure" style confirmation. 
    - The individual items in the list are to be navigation items that lead to a dedicated interface for displaying the grow guide.
    - The interface will also require a flow for creating a new grow guide.
    - The interface will also require a toggle that provides users the ability to make a guide public or private.

=== "User Allotment Interface"
    - Ability for users to create an associated allotment by providing the following information: postal code, width and length.
        - Initially this interface will just be populated with placeholder text until a user submits the required information to create an associated allotment.
    - Ability for users to update the following information for their allotment: postal code, width and length.
    
    ???+ tip "Future Improvement"
        Further interfaces relating to a users allotment will be required when implementing the functionality to provide planting recommendations.

=== "User Preference Interface"
    - Ability for users to nominate a day for for giving each type of feed.

=== "User Logout Interface"
    - Ability for users to sign out the application

<u>_**Medium Priority**_</u>

=== "User Profile Interface"
    - Ability for users to update their: first name, email address, password and country code.

=== "User Password Reset Interface"
    - Ability for users to enter a new password, after having coming from the magic link provided via email to their registered address.

<u>_**Low Priority**_</u>

=== "User Notification Interface"
    - The ability for users to control: type, method and frequency of notifications they receive. 

    !!! info "Please Note"
        This is a low priority as automated notifications are not part of the minimal viable product. Additional database tables will also be required to provide this functionality. 

---

### Family Interfaces

<u>_**Medium Priority**_</u>

=== "Botanical Group List Interface"
    - A interface that lists the different botanical groups available within the application. Where each group is a dropdown that can be select to expand/collapse. When expanded it displays the families within that group below a recommend rotate years info section.
        - Each heading within the dropdown is to be a navigation link to a page informing on that family in detail.

=== "Family Information Interface"
    - A interface that displays the surrounding information for a specific family of fruit or vegetables. 
        - The first section of information includes the families: Botanical Group, Recommended Rotation Years, Companion & Antagonist families.
        - The second section of information includes the common pests that effect the family and their treatment and prevention methods.
        - The third section of information includes the common disease that effect the family and their: symptoms, treatment and prevention methods.

---

### Grow Guide Interfaces

<u>_**High Priority**_</u>

=== "Grow Guide"
    - A interface that presents the user with a overview of a specific varieties grow guide. This interface is to double up as the form for creating/editing the grow guide also.
        - For guides a user own there is to be a button that unlocks the guide for editing.
            - This mode will require a method of ensuring users pass validation per field of the form and a method of handling submissions failures in a friendly way.

<u>_**Low Priority**_</u>

=== "Public Grow Guides"
    - A interfaces that lists all the publicly available grow guides for users to browse and use. As initial offering this screen should organize the available grow guides into botanical groups that are alphabetically sorted and the guides within each group are to be alphabetized again.
        - Long term this interface will want a comprehensive filter and search functionality.

???+ tip "Future Improvement"
    When implemented, user interfaces for generating and viewing planting recommendations will also be required.

---

### ToDo Interfaces

<u>_**High Priority**_</u>

=== "Weekly ToDo"
    - The interface that is to be considered the home page. This view will display, based on a users active varieties, their weekly tasks and where appropriate these weekly tasks are to be broken down into there specific days.
        
        - **Weekly Tasks:**
            - What varieties can be sown.
            - What varieties can be transplanted.
            - What varieties can be harvested.
            - What varieties need to be pruned.
            - What varieties can be dug up and composted.
                - This task will be based of when a variety has reached the end of its harvest period and lifecycle.
        
        - **Daily Tasks:**
            - What varieties need to be fed this week on what day.
                - Varieties that are to be fed, need to be grouped by feed type and this feed type highlighted.
            - What varieties need to be watered this week on what day.
                ???+ tip "Future Improvement"
                    Long term this task be dictated via a live weather feed based on the users allotment postal/zip code.
    
    - Each user is to be able to select a desired week in order to view the past or future, with the default load week to be the present week.

<u>_**Low Priority**_</u>

=== "Monthly ToDo"
    - This view will display a high level overview based on a users active varieties, their monthly tasks, grouped by season.
        - These tasks are to include:
            - What varieties can be sown.
            - What varieties can be transplanted.
            - What varieties can be harvested.
            - What varieties need to be pruned.
            - What varieties can be dug up and composted.
    - Each user is to be able to select a month in order to view the past or future, with the default load month to be the present.

---

## Client Side ADR

There are several aspects to consider when deciding on the appropriate technologies to meet the client side requirements of the application. On top of adhering to the modular architecture principles, just as the rest of the application, with a solution that runs on Linux based operation systems using packages and libraries that are free for commercial use, that integrate with a FastAPI RESTful API that uses JWT for authentication, all whilst delivering a progressive web application experience to many concurrent users the individual layers of the client side must also be considered in isolation.

!!! success "Outcome"

    _**Framework:**_

    - React with TypeScript
        - React is a well suited framework for developing progressive web applications that allows for a component based architecture, with several state management options, that aligns well with the applications modular design. The frameworks strong support of TypeScript also allows for the enforcement of good data integrity.
        - React hooks like useAuth and useContext also work well with the Authlib & JWT authentication flow proposed in the server side solution.

    _**UI Library:**_

    - Tailwind CSS & ShadCN
        - Tailwind provides utility first CSS, keeping styling modular and scalable. Its pairing with ShadCN allows for the provision of accessible, modern UI components.

    _**State Management:**_

    - React Query & Context API
        - As the application will mostly fetch and cache data and there is no requirement for heavy real-time collaboration React Query is sufficient to provide caching for offline mode and the Context API will manage small, app wide states, like authentication.

    _**API Communication:**_

    - Fetch with Axios
        - Axios provides good error handling with automatic request/response transformation and built in request cancellation. Making it worth the complexity trade off when compared to the native Fetch API.

    _**PWA Support:**_

    - Workbox
        - Will generate service workers for caching API responses with support for background sync.

    _**Form Handling:**_

    - React Hook Form & Zod
        - The application requires robust form validation for user-generated content. React Hook will reduce re-renders and improve performance, integrating well with TypeScript. Zod will provide a schema based validation that works with well with React Hook Form.

??? abstract "**Alternatives**"

    _**Framework:**_

    1. Vue3 with TypeScript
        - A close second option. Whilst Vue offers simpler state management when compared to React and a cleaner two-way binding for forms, plus arguably better built in support for PWA's. It is a smaller eco system that is less performant for large scale applications.
    
    1. SvelteKit
        - Svelte kit offers great performance as it compiles to vanilla JS, offering minimal runtime overhead. It also has build in support for PWAs. However, it is a immature framework with a weaker ecosystem when compared to React & Vue. This is potentially a strong option if the application develops a requirement to have an extremely small runtime overhead in order to vertically scale.

    _**UI Library:**_

    1. MUI (Material UI)
        - MUI is a feature rich component library created by Google that provides a polished UI out the box. However, it is extremely heavyweight and less customable compared to Tailwind & ShadCN.

    _**State Management:**_

    1. Redux
        - Redux is a global state management tool that scales well with strong developer tooling. The overhead is larger when compared to React Query & Context API. It is also not ideal for caching. As the application does not require extensive global state management but does require extensive caching it is not a strong choice.

    _**API Communication:**_

    1. GraphQL (Apollo Client)
        - Not a realistic choice as the server side of the application is optimized for a REST API. In the event the application migrates to a GraphQL API this would provide efficient data fetching by reducing over/under fetching issues seen in REST APIs.

    _**PWA Support:**_

    1. Service Workers without Workbox
        - Whilst this would provide full control and remove a dependency it would increase the probability of errors.

    _**Form Handling:**_
    
    1. Yup
        - Whilst Yup is a potential alternative to Zod it is less TypeScript friendly and not as flexible.

---

## Client Side Design

### Components

!!! example "Container-Presenter Pattern"

    In order to keep the components listed below clean and separate logic from presentation, the container presenter pattern is to be utilized. Allowing for a "smart" container component to handle state, API calls and business logic with a "dumb" presenter component created in order to display data. This pattern also prevents re-renders when only the UI changes, improving performance.

    1. Header
    1. Footer
    1. Dropdown Component
    1. Option Slider
    1. Vertical Accordion 
    1. Information Card
    1. Action Table
    1. Confirmation Modal
    1. Toggle

!!! example "Factory Pattern"
    
    **Form Component**

    - In order to ensure form validation is correct, inline with the applications data integrity principles, a reusable validation schema (Factory) is to be defined in a separate file. Within the form component itself this schema is to be utilized via Zod and React Hook Form in order to ensure consistent and reusable logic with minimal re-renders.

---

### API Communication

!!! example "Repository Pattern"
    
    In order to separate API logic from UI, allowing for cleaner components, easier endpoint switching and the reduction of redundant calls. API logic is to be stored in its own separate service, within these services Axios is to be used to handle data retrieval from the server. React Query is to then be implemented when retrieving data through the service in order to cache queries.

!!! example "Cache-Aside Pattern"

    In order to provide offline capabilities within the application Workbox is to be used to cache API responses on top of React Query. Improving performance and allowing for a progressive web application.

---

### Client Side Authentication

!!! example "Observer & Provider Pattern"

    As user authentication is the only required global state ContextAPI is to be used in order to setup a auth provider. React Query can then observe this provider in order to update application state.

---

### Folder Structure

!!! example "Feature-Based Folder Structure"

    Due to the application having clearly defined interfaces that can be grouped into features, a feature based folder structure makes sense, allowing related logic to be kept together.

    ``` title="Example Frontend Folder Structure"
    /src
        /features
            /growGuides
                - GrowGuideContainer.tsx
                - GrowGuidePresenter.tsx
                - growGuideService.ts
                - growGuideSchema.ts
    ```

---

### Typography

=== "Primary"

    **Primary Heading**
    
    - Oswald

    **Primary Text**
    
    - Noto Sans

=== "Fallback"

    **Fallback Heading**
    
    - Georgia

    **Fallback Text**
    
    - Verdana

---

### Color Scheme

=== "Dark Mode"

    **Primary Dark**

    - "#000000"

    **Secondary Dark**

    - "#3c4a3e"

    **Tertiary Dark**

    - "#9fafa1"

=== "Light Mode"

    **Primary Light**

    - "#ffffff"

    **Secondary Light**

    - "#f0f2e6"

    **Tertiary Light**

    - "#81885a"

=== "Interactions"

    **Primary Active**

    - "#007333"

    **Positive Action**

    - "#007a4e"

    **Neutral Action**

    - "#0076bb"

    **Negative Action**

    - "#ba2c37"