## [Automatic Installation](https://nextjs.org/docs/getting-started/installation#automatic-installation)

```
npx create-next-app@latest
```

With Typescript, ESLint, and Tailwind CSS

#### Running it (optional)

```
npm run dev
```

#### Making changes

Start by adding some initial content to `src/app/page.tsx` with:

```ts
export default function Page() {
	return <h1>Hello, Next.js!</h1>
}
```

| [`app`](https://nextjs.org/docs/app/building-your-application/routing)                     | App Router                         |
| ------------------------------------------------------------------------------------------ | ---------------------------------- |
| [`pages`](https://nextjs.org/docs/pages/building-your-application/routing)                 | Pages Router                       |
| [`public`](https://nextjs.org/docs/app/building-your-application/optimizing/static-assets) | Static assets to be served         |
| [`src`](https://nextjs.org/docs/app/building-your-application/configuring/src-directory)   | Optional application source folder |

## Routing

| Folders           | Domain              |
| ----------------- | ------------------- |
| app/page.tsx      | localhost:3000      |
| app/test/page.tsx | localhost:3000/test |

![[Pasted image 20240402135355.png]]
![[Pasted image 20240402135533.png]]
