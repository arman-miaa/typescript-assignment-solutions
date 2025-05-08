

## Blog 1: Difference Between `interface` and `type` in TypeScript

In TypeScript, we can use both `interface` and `type` to define the structure of objects. While they often seem similar, there are some key differences between them that I’ve learned while working with TypeScript.

### 🔹 interface:

I usually use `interface` when I want to describe the shape of an object.
One cool feature is that if you declare the same interface name more than once, TypeScript will automatically merge them.
Also, interfaces can extend other interfaces using `extends`.

**Example:**

```ts
interface Person {
  name: string;
  age: number;
}
```

### 🔹 type:

On the other hand, `type` is more flexible. It’s not just for objects — we can use it for union types, intersections, tuples, or even primitives.
But once you define a type with a name, you can’t use that name again to redefine it.
If you want to combine multiple types, you can use `&` to intersect them.

**Example:**

```ts
type Employee = {
  name: string;
  salary: number;
}
```

 **What I’ve learned**: If you're working with simple object structures, `interface` is the way to go. But when things get a bit more complex (like unions or intersections), `type` is a better choice.

---

## Blog 2: What is `keyof` in TypeScript and Why Use It?

While learning TypeScript, I found `keyof` to be a really useful keyword. It creates a **union of all property names** from a given object type.

### 🔹 Why do we use it?

Let’s say you want to write a function that can safely access any key of an object. Using `keyof` ensures that you don’t accidentally pass an invalid key — TypeScript will warn you right away.

### 🔹 Example:

```ts
type Person = {
  name: string;
  age: number;
};

type PersonKeys = keyof Person;
// This will be: "name" | "age"
```

Now let’s create a generic function:

```ts
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const user = { name: "Arman", age: 22 };

console.log(getProperty(user, "name")); // Output: "Arman"
```

Here, since we used `keyof`, if I try to access something like `"email"` (which doesn’t exist), TypeScript will throw an error immediately — which helps prevent bugs early.

**In short**: `keyof` makes our functions smarter and safer by ensuring we only work with valid keys of an object.

