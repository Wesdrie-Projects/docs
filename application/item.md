# Firestore Item Management Service

## Overview
This service provides CRUD operations for managing items in a Firestore collection.

## Interfaces

### `Item`
Represents an item in the collection.

```typescript
interface Item {
  id: string;        // Unique identifier for the item
  name: string;      // Name of the item
  description: string; // Detailed description of the item
  quantity: number;  // Quantity of the item
  meta: Meta;        // Metadata about the item
}
```

### `Meta`
Metadata tracking for each item.

```typescript
interface Meta {
  createdOn: Date;   // Timestamp of item creation
  updatedOn: Date;   // Timestamp of last update
}
```

## Service Methods

### `items$()`
Retrieves all items from the Firestore 'items' collection.

- **Returns:** `Observable<Item[]>`
- **Behavior:** Streams live updates of items from Firestore
- **Note:** Uses `idField: 'id'` to include document ID in returned items

### `create(item: Item)`
Creates a new item in the Firestore collection.

- **Parameters:**
  - `item`: The item to be created
- **Behavior:** 
  - Adds `meta` fields with current timestamp
  - Saves item to Firestore 'items' collection
- **Error Handling:** Logs errors to console

### `delete(itemId: string)`
Deletes an item from the Firestore collection.

- **Parameters:**
  - `itemId`: The unique identifier of the item to delete
- **Behavior:** Removes specified document from 'items' collection
- **Error Handling:** Logs errors to console

## Usage Example

```typescript
// Retrieve items
this.itemService.items$().subscribe(items => {
  console.log(items);
});

// Create a new item
const newItem: Item = {
  name: 'Sample Item',
  description: 'A test item',
  quantity: 5,
  meta: {} as Meta  // Will be automatically populated
};
this.itemService.create(newItem);

// Delete an item
this.itemService.delete('item-id-to-delete');
```

## Dependencies
- Angular's `@angular/fire/firestore`
- RxJS `Observable`
