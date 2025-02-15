# Bytebase API Sample

This is an sample app demonstrating how to use [Bytebase](https://github.com/bytebase/bytebase) API
to create and rollout a database change.

Say your organization already has a DevOps platform and you want to integrate the database change
into the development workflow. This app is for you.

The app is built with Next.js and TailwindCSS

![Bytebase API Experiment with Next.js](docs/add-issue.gif)

## Prerequisites

- Node >= v18

## Getting Started

### Step 1 - Start Bytebase

1. Check out [Self-host Bytebase via docker](https://www.bytebase.com/docs/get-started/self-host/#docker) for more information.
1. Create a [service account](https://www.bytebase.com/docs/how-to/spanner/how-to-create-a-service-account-for-bytebase/).
   Choose the `DBA` role which is sufficient for this sample.

![Service Account Create](docs/service-account-create.webp)

1. Record the service account key.

![Service Account Create](docs/service-account-key.webp)

### Step 2 - Configure and run this app

1. Clone this repository.
1. Copy `env-template.local` to `.env.local`.

   ```bash
   cp env-template.local .env.local
   ```

1. Update the env file with the created service account.

   - `NEXT_PUBLIC_BB_HOST`. The host where Bytebase is running. This usually is the [external url](https://www.bytebase.com/docs/get-started/install/external-url).
   - `NEXT_PUBLIC_BB_SERVICE_ACCOUNT`. The service account created in step 1.
   - `NEXT_PUBLIC_BB_SERVICE_KEY`. The service key created in step 1.

1. Run the following commands:

   ```bash
   pnpm i
   pnpm run dev
   ```

1. Open host with your browser to see the result.

## Implementation

### Fetch data

_You may find the following API used in `src/app/page.tsx`:_

- List all projects
  `/v1/projects`

- List all databases
  `/v1/instances/-/databases`

### Create an issue

_You may find the following API used in `src/app/components/add-issue-form.tsx` and `src/app/api/xxxx/route.ts`:_

In order to create an issue, you need to create resources **in the following order**:

1. Create a [sheet](https://github.com/bytebase/bytebase/blob/061e6faf452e1c065fb7a209c52484bd88788945/proto/gen/grpc-doc/v1/README.md#bytebase-v1-Sheet)
2. Create a [plan](https://github.com/bytebase/bytebase/blob/061e6faf452e1c065fb7a209c52484bd88788945/proto/gen/grpc-doc/v1/README.md#bytebase-v1-Plan)
3. Create an [issue](https://github.com/bytebase/bytebase/blob/061e6faf452e1c065fb7a209c52484bd88788945/proto/gen/grpc-doc/v1/README.md#bytebase-v1-Issue)
4. Create a [rollout](https://github.com/bytebase/bytebase/blob/061e6faf452e1c065fb7a209c52484bd88788945/proto/gen/grpc-doc/v1/README.md#bytebase-v1-Rollout)
