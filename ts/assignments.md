
### Assignment 1: Generic Utility Function

Create a generic function called `getFirstItem()` that accepts an array of any type and returns the first element.

Requirements:

```typescript
getFirstItem<number>([10, 20, 30]);
// Output: 10

getFirstItem<string>(["Java", "TypeScript", "React"]);
// Output: "Java"
```

Your function should work with:

```text
number[]
string[]
boolean[]
custom object[]
```

Concepts covered: **Generic Functions, `<T>`, Generic Arrays, Return Types**.

---

### Assignment 2: Generic Storage Class

Create a generic class called:

```typescript
DataStorage<T>
```

It should contain these methods:

```typescript
addItem(item: T): void

removeItem(item: T): void

getItems(): T[]
```

Example usage:

```typescript
const numberStorage =
  new DataStorage<number>();

numberStorage.addItem(10);
numberStorage.addItem(20);
numberStorage.addItem(30);

console.log(
  numberStorage.getItems()
);
```

Expected output:

```text
[10, 20, 30]
```

Also test it with strings:

```typescript
const languageStorage =
  new DataStorage<string>();

languageStorage.addItem("Java");
languageStorage.addItem("TypeScript");
```

Concepts covered: **Generic Classes, Reusability, Type Safety**.

---

### Assignment 3: Generic Repository

Create a generic repository that can manage different types of entities such as `Employee` and `Product`.

Start with:

```typescript
interface Identifiable {
  id: number;
}
```

Create:

```typescript
class Repository<T extends Identifiable>
```

The repository should provide:

```typescript
add(item: T): void

findById(id: number): T | undefined

findAll(): T[]

removeById(id: number): void
```

Create an Employee:

```typescript
interface Employee {
  id: number;
  name: string;
  department: string;
  salary: number;
}
```

Example:

```typescript
const employeeRepo =
  new Repository<Employee>();

employeeRepo.add({
  id: 101,
  name: "Amit",
  department: "IT",
  salary: 60000
});

employeeRepo.add({
  id: 102,
  name: "Rahul",
  department: "HR",
  salary: 50000
});
```

Then:

```typescript
console.log(
  employeeRepo.findById(101)
);
```

Expected result:

```text
{
  id: 101,
  name: "Amit",
  department: "IT",
  salary: 60000
}
```

Now reuse the **same Repository class** with:

```typescript
interface Product {
  id: number;
  name: string;
  price: number;
  category: string;
}
```
 training, I’d use **Assignment 1 as basic, Assignment 2 as intermediate, and Assignment 3 as the main practical assignment**.
