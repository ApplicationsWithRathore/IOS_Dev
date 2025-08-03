# TOPICS 
1. [@State , @FocusedStare, @Bindingd](#state-manage-property)
2. [Form](#form-view)


## State manage property
### @State
- `@State` property wrapper allow us to modify value inside struct, which would normally not be allowed because struct are value types.
- It move the storage out from struct to the shared storage of Swift UI { destroy and recreate struct whenever needed}
- `@State` should be use only with basic type (String, Int) and generally should not be shared with other view.
### @FocusState
- it is helping to know the focused view eg Textfield 
```swift
       TextField("Name", ...)
                .focused($fieldIsFocused)
```
```swift
struct LoginForm {
    enum Field: Hashable {
        case username
        case password
    }
    @State private var username = ""
    @State private var password = ""
    @FocusState private var focusedField: Field?
    var body: some View {
        Form {
            TextField("Username", text: $username)
                .focused($focusedField, equals: .username)
            SecureField("Password", text: $password)
                .focused($focusedField, equals: .password)
            Button("Sign In") {
                if username.isEmpty {
                    focusedField = .username
                } else if password.isEmpty {
                    focusedField = .password
                } else {
                    handleLogin(username, password)
                }
            }
        }
    }
}
```
## Form View
- To build data entry interface (settings etc)
- behave as per platform specific
- add section inside Form to group together with different titles
```swift
var body: some View {
    NavigationView {
        Form {
            Section(header: Text("Notifications")) {
                Picker("Notify Me About", selection: $notifyMeAbout) {
                    Text("Direct Messages").tag(NotifyMeAboutType.directMessages)
                    Text("Mentions").tag(NotifyMeAboutType.mentions)
                    Text("Anything").tag(NotifyMeAboutType.anything)
                }
                Toggle("Play notification sounds", isOn: $playNotificationSounds)
                Toggle("Send read receipts", isOn: $sendReadReceipts)
            }
            Section(header: Text("User Profiles")) {
                Picker("Profile Image Size", selection: $profileImageSize) {
                    Text("Large").tag(ProfileImageSize.large)
                    Text("Medium").tag(ProfileImageSize.medium)
                    Text("Small").tag(ProfileImageSize.small)
                }
                Button("Clear Image Cache") {}
            }
        }
    }
}
```
