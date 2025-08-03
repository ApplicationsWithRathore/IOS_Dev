
# CORE DATA

Core data is the local database widely used for ios applications, it will help to store permanent data for offline use and also it gives undo functionality, we can perform crud operation using core data it is fast in process when we want to update Ui using collection or table view.

## How to create Core Data Model

1. While creating a project there will be a one checkbox for core data it will automatically add some boilerplate code needed for Coredata.
2. It will automaticallycreate projectname.datamodelId (this is the main file to create entities and relationship between entities).

## Create Core data stack

''' 
class CoreDataManager {
    // Shared static instance for global access
    static let shared = CoreDataManager()

    // Persistent container
  let persistentContainer: NSPersistentContainer

    // Private initializer to enforce singleton pattern
    private init() {
        // Replace "Model" with your .xcdatamodeld file name
        persistentContainer = NSPersistentContainer(name: "ToDo_Core_Data")
        persistentContainer.loadPersistentStores { (description, error) in
            if let error = error {
                fatalError("Unable to load Core Data stack: \(error)")
            }
        }
    }

    // Main context for use on the main queue
    var context: NSManagedObjectContext {
        return persistentContainer.viewContext
    }

    // Function to save context
    func saveContext() {
        let context = persistentContainer.viewContext
        if context.hasChanges {
            do {
                try context.save()
            } catch {
                print("Error saving context: \(error.localizedDescription)")
            }
        }
    }
}
'''

1. Initialize the persistentcontainer 
    The persistent container handles the creation of the Core Data stack and is designed to be easily subclassed to add additional app-specific methods to the base Core Data functionality. Once initialized, the persistent container instance provides access to the managed object context.
2. core data method require the manage object context as an argument
    apps are not directly interact with the persistent stores 
   manage object context works as an intermediateder which hold value for temporary basis until save is not called
3. Getting an entity description
    
   
