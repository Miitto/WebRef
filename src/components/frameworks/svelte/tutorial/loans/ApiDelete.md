```ts
import { prisma } from "$lib/database.server";
import { json } from "@sveltejs/kit";

export const DELETE = async ({ params }) => {
    try {
        await prisma.loan.delete({
            where: {
                id: params.id,
            },
        });
    } catch {
        return json({ success: false });
    }
    return json({ success: true });
};
```
