# Base dev image
FROM node:24.11.1

# Environment variables for dev
ENV DIR=/app \
    NODE_ENV=production \

# Set working directory
WORKDIR $DIR

# Copy package files for dependency install
COPY package*.json ./

# Install dependencies (including devDependencies)
RUN npm ci

# Copy project source
COPY . .

# Build next.js → .next/
RUN npm run build

# Expose application port
EXPOSE 3000

# Run Next.js Dev
CMD ["npm", "run", "start"]