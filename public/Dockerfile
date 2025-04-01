# Use an official Node.js runtime (Example for Node.js app)
FROM node:18

# Set the working directory
WORKDIR /app

# Copy package files and install dependencies
COPY package*.json ./
RUN npm install

# Copy the rest of the application
COPY . .

# Expose the application port
EXPOSE 3000

# Run the application
CMD ["npm", "start"]
