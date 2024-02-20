---
title: (E)ER-Exmaple
---

# Assignment 1

## Description

- The goal of this assignment is to design a conceptual schema using the (E)ER Data model.  

## (E)ER data model (50 points)

- Design a schema that incorporates the specification described below as efficiently as possible.
- You should submit a written diagram of your schema design using the notation given in the class.
- In this diagram, indicate all the classes, subclasses, relationships (weak & strong), relationship cardinalities and degrees, total participations, attributes, and primary keys.
- In addition, specify whether each attribute is single-valued or multi-valued, stored or derived, and atomic or composite.
- In your design, you can make and state reasonable assumptions if they are not specified in the specification.

## Design Specification

- Yelp is a local business directory service and review site with social networking features.
- It allows users to give ratings and review businesses.
- You are going to design the database system for [Yelp](www.yelp.com).
- It should store and manage the following information but it is not exactly same as real Yelp website.
- However, if you have ambiguous parts you can assume data type based on real Yelp system:

## Yelp User

- A Yelp user has a unique yelp ID, first name, last name, gender, birthdate, birthplace, age, email, a profile picture, and list of friend ids.
  - STRONG ENTITY PRIMARY KEY: yelp_id
  - ATTRIBUTE (simple, single-valued, stored): first_name
  - ATTRIBUTE (simple, single-valued, stored): last_name
  - ATTRIBUTE (simple, single-valued, stored): gender
  - ATTRIBUTE (simple, single-valued, stored): birthdate
  - ATTRIBUTE (simple, single-valued, stored): birthplace
  - ATTRIBUTE (simple, single-valued, derived[birthdate]): age
  - ATTRIBUTE (simple, single-valued, stored): email
  - ENTITY: Photo
    - RELATIONSHIP: Has
    - PARTICIPATION: Partial 1:1 Partial
  - ENTITY: Yelp User
    - RELTIONSHIP: Friend
      - ATTRIBUTE (simple, multivalued, stored): friend_id
    - PARTICIPATION: Partial M:N Partial
- Yelp users can be complimented by their friends.
  - ENTITY: Yelp User
    - RELATIONSHIP: Compliment
    - PARTICIPATION: Partial M:N Partial
- A Yelp user can rate any business on a scale of 1-5 and provide reviews.
  - ENTITY: Business
    - RELATIONSHIP: Rate
    - PARTICIPATION: Partial 1:M Partial
- A user has an "Activity Wall" where 10 most recent Yelp reviews by user's friends are posted on the wall when the user “follows” her friend’s activities.
  - ENTITY: Review
    - Relationship: Activity Wall
    - PARTICIPATION: Partial 1:M Partial
- In addition, the user can check-in to a particular business.

## Reviews

- Review has an unique ID, publish date, and textual content where the content can be text, photo, or a short video.
  - STRONG ENTITY PRIMARY KEY: review_id
  - ATTRIBUTE (simple, single-valued, stored): publish_date
  - ATTRIBUTE (composite, single-valued, stored): content
    - ATTRIBUTE (simple, single-valued, stored): text
    - ATTRIBUTE (simple, single-valued, stored): photo
    - ATTRIBUTE (simple, single-valued, stored): video
- It has one author and belongs to one business.
- Also a review has number of stars and number of total votes.
    - ATTRIBUTE (simple, single-valued, stored): num-stars
    - ATTRIBUTE (simple, single-valued, stored): num-votes
- Votes can be categorized as useful and non-useful with a list of users that voted for each of these categories.
  - ENTITY: Yelp Users
    - RELATIONSHIP: Vote
      - ATTRIBUTE (simple, multivalued, stored): category
      - ATTRIBUTE (simple, multivalued, stored): user-id
- Moreover, a review has a list of comments where each comment has an author, textual content, and date.
  - ATTRIBUTE (composite, multivalued, stored): comments
    - ATTRIBUTE (simple, single-valued, stored): author
    - ATTRIBUTE (simple, single-valued, stored): content
    - ATTRIBUTE (simple, single-valued, stored): date

## Business
- A business has an ID, address (street, state, zip code, latitude, longitude), number of reviews, and stars.
  - STRONG ENTITY PRIMARY KEY: business_id
  - ATTRIBUTE (composite, single-valued, stored): address
    - ATTRIBUTE (simple, single-valued, stored): street
    - ATTRIBUTE (simple, single-valued, stored): state
    - ATTRIBUTE (simple, single-valued, stored): zip code
    - ATTRIBUTE (simple, single-valued, stored): latitude
    - ATTRIBUTE (simple, single-valued, stored): longitude
  - ATTRIBUTE (simple, single-valued, stored): num-reviews
  - ATTRIBUTE (simple, single-valued, stored): num-stars
- Also each business has hours and days of operation.
  - ATTRIBUTE (composite, multivalued, stored): operation
    - ATTRIBUTE (simple, single-valued, stored): open-time
    - ATTRIBUTE (simple, single-valued, stored): close-time
    - ATTRIBUTE (simple, single-valued, stored): day
- Other attributes of business include parking type (street, garage, lot, or valet), and ambient type (romantic, classy, touristy, or casual).
  - ATTRIBUTE (simple, single-valued, stored): parking-type
  - ATTRIBUTE (simple, single-valued, stored): ambient-type
- A business maintains a list of check-in IDs. A review is belonged to a business.

## Business Category

- Each business has one category. Business category has an ID, name, and a list of subcategories. Some categories and their subcategories are as follow:
  - Health & Medical: Dentists, Optometrists, Hospital, Doctors, Physical Therapy, and Allergists
  - Restaurants: Bars, Sandwiches, Diners, Burgers, Pizza, Seafood, and Salad
  - Hotels & Travel: Bed & Breakfast, Event Planning & Services, and Car Rentals
  - Shopping: Flowers & Gifts, Art Supplies, Hardware Stores, Drugstores, Convenience Stores, Department Stores, Home Services, Outlet Stores, and Florists
  - Food: Bakeries, Coffee & Tea, Grocery, and Food Delivery Services
  - Beauty & Spas: Cosmetics & Beauty Supply, and Fashion
  - Fitness & Instruction: Active Life, Gyms, Weight Loss Centers, Trainers, Pilates, and Nutritionists
  - Education: Colleges & Universities, Middle Schools & High Schools, Adult Schools, Specialty Schools, Dance Studios, Preschools, Child Care & Day Care.
- You may choose only two of the above categories and their corresponding subcategories for demonstration purposes.

## Photo

- A Photo has a unique ID, an author, a description, location, and a list of users who “liked” the photo.
  - STRONG ENTITY PRIMARY KEY: photo_id
  - ATTRIBUTE (simple, single-valued, stored): author
  - ATTRIBUTE (simple, single-valued, stored): description
  - ATTRIBUTE (simple, single-valued, stored): location
  - ENTITY: Yelp User
    - Relationship: Like
      - ATTRIBUTE (simple, multivalued, stored): User
- Each photo is either a business photo or a personal photo.
  - CONTRAINTS: Disjoin Set
    - ENTITY: Buisness
    - ENTITY: PERSONAL
- A business photo is only visible to a user who checked into that particular business.
- A business photo is belonged to a business.

## Check-In

- A check-in has an ID and check-in info.
- A check-in belongs to a business.
- A user can check-in to a business multiple times.