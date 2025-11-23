# Stage 1 — build
FROM node:22-alpine AS builder

WORKDIR /app

COPY package*.json ./

RUN npm install --production=false

COPY . .

RUN npm run build

# Stage 2 — production
FROM node:22-alpine AS runner
WORKDIR /app

ENV NODE_ENV=production
ENV PORT=5000

COPY --from=builder /app/dist ./dist
COPY package*.json ./
RUN npm install --production

EXPOSE 5000
CMD ["node", "dist/server.js"]