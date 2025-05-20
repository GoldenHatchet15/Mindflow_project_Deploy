FROM node:18-alpine

WORKDIR /app

# Copy package files first (better caching)
COPY package*.json ./
RUN npm install --production  # Use --production to avoid dev dependencies

# Copy the rest of the application
COPY . .

# Set environment variables
ENV NODE_ENV=production
ENV PORT=5000

# Expose port for documentation purposes
EXPOSE 5000

# Use a health check
HEALTHCHECK --interval=30s --timeout=10s --start-period=5s --retries=3 \
  CMD wget --no-verbose --tries=1 --spider http://localhost:5000/api/health || exit 1

CMD ["node", "server.js"]