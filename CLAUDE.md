# Chain of Command

Chain of Command is a social deduction game built into a iOS application, with a server component. This monorepo contains source code for both.

# Background on Game and Rules

See the Manual (Chain_of_Command_Manual_v1.pdf) and Role Book (Chain_of_Command_Role_Book_v1.pdf) for details on the game and its rules.

# iOS Application

The application is built natively for iOS using Swift and SwiftUI. It is designed for modern iPhones with 5G capability (containing Ultra Wideband capability), especially exploiting the [NearbyInteraction Framework](https://developer.apple.com/documentation/nearbyinteraction) to detect the relative positions of players in a game. The application is designed to be used in a social setting, with players sitting around a table and also in a free-roam setting.

# Server Component

The tech stack for the server component is still undecided, and can be flexible to the needs of the project.
