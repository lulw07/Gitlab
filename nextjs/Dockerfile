FROM docker.io/node:19-alpine AS base

#Install dependencies
FROM base AS dependencies
WORKDIR /src

COPY src/package.json src/yarn.lock* src/package-lock.json* src/pnpm-lock.yaml* ./
RUN \
  if [ -f yarn.lock ]; then yarn --frozen-lockfile; \
  elif [ -f package-lock.json ]; then npm ci; \
  elif [ -f pnpm-lock.yaml ]; then yarn global add pnpm && pnpm i; \
  else echo "Lockfile not found." && exit 1; \
  fi

#Build source code
FROM base AS builder
WORKDIR /src

COPY --from=dependencies /src/node_modules ./node_modules
COPY src ./

RUN npm run build

#Build production
FROM base AS runner
WORKDIR /src

RUN addgroup -g 1001 -S nodejs
RUN adduser -S nextjs -u 1001

COPY --from=builder /src/next.config.js ./
COPY --from=builder /src/package.json ./package.json
COPY --from=builder /src/public ./public
COPY --from=builder --chown=nextjs:nodejs /src/.next/standalone ./
COPY --from=builder --chown=nextjs:nodejs /src/.next/static ./.next/static

USER nextjs

EXPOSE 3000
ENV PORT 3000

CMD ["node", "server.js"]