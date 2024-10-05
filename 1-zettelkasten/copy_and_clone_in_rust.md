Created on 2024-09-14_15-12-44

## 📔 Notes

### Difference between Clone trait and Copy trait in Rust

- `Copy` -> implicit duplication

eg. 
```rust

let x = 5;
let y = x; // implicit duplication

```

- happens automatically during assignment or function call

- `Clone` -> explicit duplication

eg.
```rust

let x = String::from("hello");
let y = x.clone(); // explicit duplication

```

- requires programmer to deliberately request a copy

## 🔗 Links

- [[Tech]]
