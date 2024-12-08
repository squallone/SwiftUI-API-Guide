# SwiftUIExamples

## List

A List in SwiftUI is a view that displays a scrollable list of data. It’s similar to UITableView in UIKit, but it is simpler and more declarative. Let's go through examples from basic to advanced.

### Custom Rows
Customize each row by defining a ForEach block or using custom views:

```swift 
struct CustomRowListView: View {
    struct Fruit: Identifiable {
        let id = UUID()
        let name: String
        let color: Color
    }

    let fruits = [
        Fruit(name: "Apple", color: .red),
        Fruit(name: "Banana", color: .yellow),
        Fruit(name: "Cherry", color: .red)
    ]

    var body: some View {
        List(fruits) { fruit in
            HStack {
                Circle()
                    .fill(fruit.color)
                    .frame(width: 20, height: 20)
                Text(fruit.name)
                    .font(.headline)
            }
        }
    }
}

```

![image](https://github.com/user-attachments/assets/a9798957-8cca-4371-a25c-7630205c2e53)

### Sections
Organize data into sections using Section:


```swift
struct SectionedListView: View {
    let fruits = ["Apple", "Banana", "Cherry"]
    let vegetables = ["Carrot", "Broccoli", "Spinach"]

    var body: some View {
        List {
            Section(header: Text("Fruits")) {
                ForEach(fruits, id: \.self) { fruit in
                    Text(fruit)
                }
            }
            Section(header: Text("Vegetables")) {
                ForEach(vegetables, id: \.self) { vegetable in
                    Text(vegetable)
                }
            }
        }
    }
}


```

![image](https://github.com/user-attachments/assets/4010f2bd-0aa2-4413-ad5b-ed0d3b714ab8)


### Editable List
Enable row reordering and deletion using .onMove and .onDelete:

```swift
struct EditableListView: View {
    @State private var items = ["Item 1", "Item 2", "Item 3"]

    var body: some View {
        NavigationView {
            List {
                ForEach(items, id: \.self) { item in
                    Text(item)
                }
                .onDelete(perform: deleteItem)
                .onMove(perform: moveItem)
            }
            .navigationTitle("Editable List")
            .toolbar {
                EditButton()
            }
        }
    }

    func deleteItem(at offsets: IndexSet) {
        items.remove(atOffsets: offsets)
    }

    func moveItem(from source: IndexSet, to destination: Int) {
        items.move(fromOffsets: source, toOffset: destination)
    }
}
```

![image](https://github.com/user-attachments/assets/9f7e3460-bca3-4f3b-83b9-6e6fcbfa37c0)
