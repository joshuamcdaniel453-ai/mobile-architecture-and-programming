# CS 360 Mobile Architecture and Programming

## Portfolio artifact

[StockKeeper Android Studio project](StockKeeper_AndroidStudio_Project.zip) contains the Java app source, programmatically constructed UI, SQLite database implementation, Gradle configuration, tests, and build documentation. The optional [inventory app launch plan](StockKeeper_Inventory_Launch_Plan.docx) is also included.

StockKeeper is a coursework prototype. Its source README explains that the UI was created fresh because the earlier Project Two UI project was not available. This artifact therefore does not establish continuity with the original Project Two design.

## App requirements and user needs

StockKeeper was designed to help small shop owners, stockroom workers, and household organizers track inventory without a complex warehouse system. The app supports account creation and sign-in, viewing inventory, adding and editing items, adjusting quantities, and deleting entries. SQLite stores inventory and alert preferences locally and separates them by account. Optional SMS alerts notify a chosen recipient when an item becomes out of stock. Core inventory features remain available when SMS permission is denied.

## Screens and user-centered design

The app has a login and account-creation screen, an inventory grid with add and edit dialogs, and an alert-settings screen. Item cards show names, quantities, and text stock indicators. Quick quantity buttons reduce the steps needed for routine updates, while deletion confirmation helps prevent accidental removal. An empty-state message explains how to add the first item. Input validation provides feedback for invalid quantities, account information, and phone numbers.

The design keeps common inventory actions visible and makes alerts optional. Shared spacing, readable labels, and minimum button sizes support consistency. These choices address the intended tasks, but successful usability and accessibility still need confirmation through emulator, device, and user testing.

## Coding approach and transferable strategies

The code separates responsibilities among activities, database access, validation rules, password hashing, and SMS handling. InventoryRules centralizes quantity validation and stock-transition decisions, while InventoryDatabase handles persistence and account filtering. Database work and password checks run on a worker thread rather than blocking the UI.

This structure provides a practical approach for future projects: define the data model, separate business rules from screen code, and keep slow operations off the main thread. Centralizing shared rules also makes behavior easier to test and change without repeating logic across screens.

## Testing and what it revealed

The supplied build record reports four passing JUnit tests covering quantity boundaries, names and phone numbers, positive-to-zero stock transitions, and salted password hashing and verification. It also reports successful Java compilation against Android API 36 and XML parsing. These checks provide evidence about individual rules and source consistency, including rejection of invalid quantities and prevention of repeated alerts when an item stays at zero.

The complete Gradle APK build was not successful: the documented Windows AAPT2 crash blocked resource linking. The tests were run directly with javac and JUnit, rather than through a completed Gradle test pipeline. Database instrumentation compiled but was not executed. Emulator testing, physical-device testing, SMS delivery, and final Android lint results remain unverified. Testing is important because passing logic tests does not prove that the packaged app installs, displays correctly, or handles Android permissions at runtime. The included TESTING.md lists those remaining checks.

## Challenge and innovation

One design challenge was supporting optional out-of-stock alerts without making inventory depend on SMS permission. The implementation keeps inventory operations available when permission is denied or texting is unsupported. It also distinguishes a newly empty item from an item that was already at zero, reducing duplicate alert requests.

The project separates coursework and Play-oriented build variants. The Play variant removes direct SMS permission and disables texting; a replacement notification feature remains future work. This illustrates how build configuration can support different distribution requirements without duplicating the inventory implementation.

## Strongest component

The inventory data and validation layer is a particular strength of the artifact. It combines account-scoped queries, parameterized database operations, quantity constraints, and testable stock-transition rules. Together, these choices connect the user-facing actions to consistent stored data and alert decisions. I would build on this foundation by completing database instrumentation and end-to-end testing before treating the app as ready for release.

## Opening the project

Extract the ZIP and open the StockKeeper folder containing settings.gradle in Android Studio. Follow its README.md for JDK, SDK, build-variant, and execution instructions. Read BUILD_STATUS.md and TESTING.md for the recorded results and remaining work. No APK is included.

## AI assistance acknowledgment

OpenAI ChatGPT/Codex was used to inspect the supplied files and organize this portfolio reflection. The original project and launch plan also disclose AI assistance with code and documentation. Statements about validation are based on the supplied build record; no additional app tests were performed while preparing this README. I should review the reflection to confirm that it accurately represents my understanding and contributions.
