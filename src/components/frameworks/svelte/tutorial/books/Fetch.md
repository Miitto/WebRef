```ts
import { prisma } from "$lib/database.server";
import type { PageServerLoad } from "./$types";

export const load: PageServerLoad = async () => {
    const books = await prisma.book.findMany(); // [!code ++]
    const authors = await prisma.author.findMany();

    return {
        authors,
        books, // [!code ++]
    };
};
```
