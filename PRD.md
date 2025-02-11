# 타베로그 Product Requirements Document (PRD)

## Overview
타베로그 is a web service for writing and reading restaurant reviews. Users can create, read, update, and delete (CRUD) reviews. The service will integrate with a map API to display restaurant locations and allow users to leave ratings and reviews.

## Objectives
- Provide a user-friendly interface for writing and reading restaurant reviews.
- Integrate with a map API to display restaurant locations.
- Allow users to perform CRUD operations on reviews.
- Enable users to rate restaurants.

## Features

### User Authentication
- Users can sign up, log in, and log out.
- Password recovery and reset functionality.

### Restaurant Reviews
- Users can create, read, update, and delete reviews.
- Reviews include a rating (1-3 stars), text, and optional photos.
- Users can view a list of reviews for a specific restaurant.

### Map Integration
- Display restaurant locations on a map using a map API (e.g., Google Maps, Mapbox).
- Users can search for restaurants by name or location.
- Clicking on a restaurant marker on the map shows basic information and a link to the reviews.

### Rating System
- Users can rate restaurants on a scale of 1 to 3 stars.
- Average rating is displayed for each restaurant.

## Technical Requirements

### Frontend
- Framework: React.js + next.js
- Responsive design for mobile and desktop

### Backend
- Framework: Django
- Database: MySql or postgreSQL
- Authentication: JWT (JSON Web Tokens)

### Map API
- Integration with Google Maps API or Mapbox API

### Hosting
- Personal physical PC with Ubuntu
- Domain routing via a router
- SSL implementation for secure connections

## Non-Functional Requirements
- Performance: The application should load within 3 seconds.
- Security: Protect user data with encryption and secure authentication.
- Scalability: The system should handle up to 10,000 concurrent users.
- Usability: The interface should be intuitive and easy to use.

## Milestones
1. **MVP (Minimum Viable Product)**
   - User authentication
   - Basic CRUD operations for reviews
   - Map integration with basic restaurant markers
   - Basic rating system

2. **Beta Release**
   - Enhanced UI/UX
   - Advanced search and filter options
   - User profile management

3. **Full Release**
   - Performance optimizations
   - Additional features based on user feedback
   - Marketing and user acquisition strategies

## Risks and Mitigations
- **Data Security**: Implement strong encryption and secure authentication methods.
- **API Limitations**: Monitor API usage and handle rate limiting gracefully.
- **Scalability**: Design the system to scale horizontally to handle increased load.

## Conclusion
타베로그 aims to provide a comprehensive platform for restaurant reviews with seamless map integration and a robust rating system. By following this PRD, we can ensure a structured and efficient development process.

