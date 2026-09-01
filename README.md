# Grocery Store Management System (Assignment 2)

A console-based grocery store manager written in Java. It keeps an inventory of
products and a shopping cart, and supports undoing the most recent
add-to-cart action.

## Data structures used

| Structure | Where | Purpose |
| --- | --- | --- |
| Singly linked list | `CartList` / `CartNode` | Holds the items currently in the cart |
| Generic linked-list stack | `LinkedListStack<T>` | Stores `CartAction` history so the last add can be undone |
| Dynamic array (`ArrayList`) | `InventoryManager` | Holds the product catalogue loaded from file |

## Source files

| File | Responsibility |
| --- | --- |
| `Main.java` | Entry point; prints the menu and dispatches each choice |
| `Product.java` | Product model: `id`, `name`, `price`, `stock` |
| `InventoryManager.java` | Add / remove / search / update products; load and save the inventory file |
| `CartList.java`, `CartNode.java` | Shopping cart as a singly linked list; keeps inventory stock in sync |
| `CartAction.java` | Immutable record of one add-to-cart action, used by the undo stack |
| `LinkedListStack.java` | Generic stack backing the undo feature |
| `inventory.txt` | Data file, one product per line as `ID,Name,Price,Stock` |

## Build and run

Requires a JDK (Java 8 or newer). From the repository root:

```bash
javac -d out *.java
java -cp out Assignment2.Main
```

On start-up the program loads `inventory.txt` (it first looks for
`Assignment2/inventory.txt`, then falls back to `inventory.txt` in the current
directory).

## Menu options

```
1  - Load inventory from file (reload)
2  - Display all products
3  - Search product by ID
4  - Search product by name
5  - Add new product
6  - Remove product
7  - Update stock quantity
8  - Save inventory to file
9  - Add item to cart
10 - View cart
11 - Remove item from cart
12 - Update item quantity in cart
13 - Clear cart (restore stock)
14 - Undo last cart addition
15 - Generate bill / checkout
16 - Save and exit
```

## Notes on behaviour

- Adding an item to the cart immediately reduces the product's stock; removing
  it, clearing the cart, or undoing the addition restores that stock.
- Checkout (option 15) clears the cart **without** restoring stock, making the
  sale final, then offers to save the inventory.
- The inventory cannot be reloaded (option 1) while the cart is non-empty.
