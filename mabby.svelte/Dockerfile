FROM node:18-alpine

# Set the working directory
WORKDIR /mabby.svelte

# Copy package.json and package-lock.json (if available)
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build your SvelteKit app
RUN npm run build

# Expose the port your SvelteKit app will run on
EXPOSE 3000

# Start your SvelteKit app in production mode
CMD ["node", ".svelte-kit/output/server/index.js"]