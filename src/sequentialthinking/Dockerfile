FROM node:18-alpine

WORKDIR /app

# Copy package.json and package-lock.json files
COPY src/sequentialthinking/package*.json ./

# Install dependencies
RUN npm install

# Copy TypeScript configuration files
COPY tsconfig.json /tsconfig.json

# Copy source code
COPY src/sequentialthinking/*.ts ./

# Build the application
RUN npm run build

# Set environment variables
ENV NODE_ENV=production
ENV HOST=0.0.0.0
ENV PORT=3000

# Expose port
EXPOSE 3000

# Run the application
CMD ["node", "dist/index.js", "--transport", "http", "--port", "3000", "--host", "0.0.0.0"]
