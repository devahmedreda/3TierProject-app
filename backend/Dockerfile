FROM node:18-alpine

WORKDIR /app

# Copy dependency file first for better layer caching
COPY package.json .

# Install production dependencies only
RUN npm install --production

# Copy application code
COPY server.js .

EXPOSE 8081

# Run as non-root user for security
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
USER appuser

CMD ["node", "server.js"]
