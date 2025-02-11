# Dockerize
Dockerize

# Tabelog-like Restaurant Review Service

This project is a web service for writing restaurant reviews, similar to Tabelog. It uses the Google Maps API to allow users to search for restaurants and perform CRUD operations on restaurant data. Users can also leave ratings and reviews for each restaurant.

## Features

- **Google Maps Integration**: Search for restaurants using the Google Maps API.
- **CRUD Operations**: Create, read, update, and delete restaurant information.
- **User Reviews**: Leave ratings and reviews for restaurants.

## Getting Started

1. Clone the repository:
2. SSH 공개키 인증 후 
   ```bash
   git clone git@github.com:UMukMin/Dockerize.git
   cd umm-dockerize
   ```

3. Install dependencies:
   ```bash
   npm install
   ```

4. Set up environment variables:
   Create a `.env` file in the root directory and add your Google Maps API key:
   ```env
   NEXT_PUBLIC_GOOGLE_MAPS_API_KEY=your_google_maps_api_key
   ```

5. Run the development server:
   ```bash
   npm run dev
   ```

6. Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

## Usage

- Use the search box to find restaurants on the map.
- Click on a restaurant to view its details.
- Register a new restaurant by clicking the "Register Restaurant" button.
- Leave a rating and review for a restaurant.

## Contributing

Contributions are welcome! Please open an issue or submit a pull request.

## License

This project is licensed under the MIT License.
