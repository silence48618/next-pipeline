###############################################
# Builder Stage
###############################################
FROM node:24.11.1 AS builder

ENV DIR=/app \
    NODE_ENV=production

WORKDIR $DIR

# Copy dependencies files
COPY package*.json ./

# Install only production dependencies + required build deps
RUN npm ci

# Copy full project
COPY . .

# Build next.js → .next/
RUN npm run build


###############################################
# Production Stage
###############################################
FROM node:24-alpine3.21 AS production

ENV DIR=/app \
    NODE_ENV=production

WORKDIR $DIR

# Copy production build from builder
COPY --from=builder /app/.next/standalone ./
COPY --from=builder /app/.next/static ./.next/static
COPY --from=builder /app/public ./public

# Expose the Next.js port
EXPOSE 3000

# Run Next.js production server
CMD ["node", "server.js"]