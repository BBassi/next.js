---
description: Next.js supports TypeScript by default and has built-in types for pages and the API. You can get started with TypeScript in Next.js here.
---

# TypeScript

<details>
  <summary><b>Examples</b></summary>
  <ul>
    <li><a href="https://github.com/zeit/next.js/tree/canary/examples/with-typescript">TypeScript</a></li>
  </ul>
</details>

Next.js provides an integrated [TypeScript](https://www.typescriptlang.org/) experience out of the box, similar to an IDE.

To get started, create an empty `tsconfig.json` file in the root of your project:

```bash
touch tsconfig.json
```

Next.js will automatically configure this file with default values. Providing your own `tsconfig.json` with custom [compiler options](https://www.typescriptlang.org/docs/handbook/compiler-options.html) is also supported.

> Next.js uses Babel to handle TypeScript, which has some [caveats](https://babeljs.io/docs/en/babel-plugin-transform-typescript#caveats), and some [compiler options are handled differently](https://babeljs.io/docs/en/babel-plugin-transform-typescript#typescript-compiler-options).

Then, run `next` (normally `npm run dev`) and Next.js will guide you through the installation of the required packages to finish the setup:

```bash
npm run dev

# You'll see instructions like these:
#
# Please install typescript, @types/react, and @types/node by running:
#
#         yarn add --dev typescript @types/react @types/node
#
# ...
```

You're now ready to start converting files from `.js` to `.tsx` and leveraging the benefits of TypeScript!.

> A file named `next-env.d.ts` will be created in the root of your project. This file ensures Next.js types are picked up by the TypeScript compiler. **You cannot remove it**, however, you can edit it (but you don't need to).

> Next.js `strict` mode is turned off by default. When you feel comfortable with TypeScript, it's recommended to turn it on in your `tsconfig.json`.

By default, Next.js reports TypeScript errors during development for pages you are actively working on. TypeScript errors for inactive pages **do not** block the development process.

If you want to silence the error reports, refer to the documentation for [Ignoring TypeScript errors](/docs/api-reference/next.config.js/ignoring-typescript-errors.md).

## Static Generation and Server-side Rendering

For `getStaticProps`, `getStaticPaths`, and `getServerSideProps`, you can use the `GetStaticProps`, `GetStaticPaths`, and `GetServerSideProps` types respectively:

```ts
import { GetStaticProps, GetStaticPaths, GetServerSideProps } from 'next'

export const getStaticProps: GetStaticProps = async context => {
  // ...
}

export const getStaticPaths: GetStaticPaths = async () => {
  // ...
}

export const getServerSideProps: GetServerSideProps = async context => {
  // ...
}
```

> If you're using `getInitialProps`, you can [follow the directions on this page](/docs/api-reference/data-fetching/getInitialProps.md#typescript).

## API Routes

The following is an example of how to use the built-in types for API routes:

```ts
import { NextApiRequest, NextApiResponse } from 'next'

export default (req: NextApiRequest, res: NextApiResponse) => {
  res.status(200).json({ name: 'John Doe' })
}
```

You can also type the response data:

```ts
import { NextApiRequest, NextApiResponse } from 'next'

type Data = {
  name: string
}

export default (req: NextApiRequest, res: NextApiResponse<Data>) => {
  res.status(200).json({ name: 'John Doe' })
}
```

## Custom `App`

If you have a [custom `App` ](/docs/advanced-features/custom-app), you can use the built-in type `AppProps` and change file name to `./pages/_app.tsx` like so:

```ts
import { AppProps } from 'next/app'

function MyApp({ Component, pageProps }: AppProps) {
  return <Component {...pageProps} />
}

export default MyApp
```
