# Use the official Node.js 20 image
From node:20

# Create app directory
WORKDIR /app

# Install app dependencies
COPY package*.json ./
RUN npm install

# Bundle app source
COPY . .

# Expose the port, the app runs on
EXPOSE 3000

# RUN the app
CMD [ "npm", "start" ]