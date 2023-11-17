# Use a smaller base image
FROM node:20-alpine as build

WORKDIR /usr/src/app

# Copy just the package.json and package-lock.json files first
COPY package*.json ./

# Install dependencies, including production dependencies only
RUN npm install --production

# Create a dummy index.js file to prevent issues during the build
RUN echo "console.log('This is a dummy file');" > index.js

# Stage 2: Create the final image
FROM node:20-alpine

WORKDIR /usr/src/app

# Copy only what's necessary from the build stage
COPY --from=build /usr/src/app/node_modules ./node_modules
COPY --from=build /usr/src/app/package*.json ./

# Remove the dummy index.js file
RUN rm -f index.js

# Copy the rest of the application
COPY . .

EXPOSE 3000

CMD ["node", "index.js"]

