# JsonToTypescript

### JSON → TypeScript Model CLI

[![npm version](https://img.shields.io/npm/v/json-to-typescript.svg)](https://www.npmjs.com/package/json-to-typescript)
[![npm downloads](https://img.shields.io/npm/dw/json-to-typescript.svg)](https://www.npmjs.com/package/json-to-typescript)
[![license](https://img.shields.io/npm/l/json-to-typescript.svg)](./LICENSE)


Convert raw JSON into clean, readable TypeScript types or interfaces in seconds.

![alt text](https://github.com/KevinG115/JsonToTypescript/raw/main/app/assets/json-to-typescript.png)
## Features

- **One-step generation**: paste JSON and press Enter to generate a `.ts` file.
- **Readable names**: nested types are named from JSON keys  
  e.g. `profile` → `Profile`, `projects` → `Project[]`, `settings.notifications` → `Notifications`.
- **Smart inference**
    - `null` becomes `any` (and `any` dominates unions).
    - ISO-like date strings become `string | Date`.
    - Arrays of short token-like strings become string-literal unions, e.g. `("admin" | "editor")[]`.
- **File naming**: output file uses the model name lowercased, e.g. `User` → `user.ts`.
- **No dependencies**: single-file Node CLI.

## Install

```bash
npm install -g json-to-typescript
```

## Usage

### Interactive (paste JSON)
```bash
json-to-typescript
# Prompts:
# Model name (e.g., User, OrderItem): User
# Paste JSON and press Enter when done:
# { ...your JSON... }
# => generates user.ts in the current directory
```

### From a file
```bash
json-to-typescript --model-name Order --input-json ./order.json
```

### With options
- `--interface` → generate `interface` instead of `type`
- `--no-dates` → don't convert ISO strings to `Date`
- `--no-color` → plain log output
- `--out path.ts` → specify output file path

## Example

Input JSON:

```json
{
  "id": 123,
  "name": "Patrick",
  "profile": { "bio": "Dev", "age": 30 },
  "tags": ["typescript", "node"]
}
```

Output:

```ts
export type Profile = {
  age: number;
  bio: string;
};

export type User = {
  id: number;
  name: string;
  profile: Profile;
  tags: ("typescript" | "node")[];
};
```

## Contributing

PRs welcome!

---

## Future Enhancements

- **Nested file output** → split models into multiple `.ts` files instead of one big file
- **JSON → Java**
    - Generate POJOs with optional Lombok annotations.
- **JSON → Rust**
    - Generate `struct`s with optional `serde` annotations for serialization.
- **JSON → Python**
    - Generate Pydantic models (ideal for FastAPI and modern Python backends).
- **Java → TypeScript**
    - Translate existing Java POJOs into matching TypeScript interfaces.
    - Config file support to specify which POJOs to include for translation.
- **VS Code extension** → right-click JSON → *Generate TypeScript Interface*
- **Web playground** → paste JSON in browser → copy TS interface


---

## License

MIT © Kevin Gleeson