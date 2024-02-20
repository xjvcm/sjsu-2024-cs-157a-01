---
title: Assignment 01
---

## Description

The goal of this assignment is to design a conceptual schema using the (E)ER Data model.

## (E)ER data model

Design a schema that incorporates the specification described below as efficiently as possible. You should submit a
written diagram of your schema design using the notation given in the class. In this diagram, indicate all the classes,
subclasses, relationships (weak & strong), relationship cardinalities and degrees, total/partial participation,
attributes, and primary keys. In addition, specify whether each attribute is single-valued or multi-valued, stored or
derived, and atomic or composite. In your design, you can make and state reasonable assumptions if they are not
specified in the specification.

## Design Specification

Yelp is a local business directory service and review site with social networking features. It allows users to give
ratings and review businesses. You are going to design the database system for [Yelp](www.yelp.com). It should store and
manage the following information but it is not exactly same as real Yelp website. However, if you have ambiguous parts
you can assume data type based on real Yelp system:

## Yelp User

A Yelp user has a unique yelp ID, first name, last name, gender, birthdate, birthplace, age, email, a profile picture,
and list of friend ids. Yelp users can be complimented by their friends. A Yelp user can rate any business on a scale of
1-5 and provide reviews. A user has an " Activity Wall" where 10 most recent Yelp reviews by user's friends are posted
on the wall when the user “follows” her friend’s activities. In addition, the user can check-in to a particular
business.

| Description                          | Name            | Attribute Types                  | Key         |
|--------------------------------------|-----------------|----------------------------------|-------------|
| A Yelp user has a unique Yelp ID.    | user_id         | Atomic / Single-Valued / Stored  | Primary Key |
| A Yelp user has a first name.        | First Name      | Atomic / Single-Valued / Stored  |             |
| A Yelp user has a last name.         | Last Name       | Atomic / Single-Valued / Stored  |             |
| A Yelp user has a gender.            | Gender          | Atomic / Single-Valued / Stored  |             |
| A Yelp user has an an age.           | Age             | Atomic / Single-Valued / Derived |             |
| A Yelp user has an email.            | Email           | Atomic / Single-Valued / Stored  |             | 
| A Yelp user has a profile picture.   | Profile Picture | Atomic / Signle-Valued / Stored  |             |
| A Yelp user has a list of friend ids | friend_id       | Atomic / Multivalued / Stored    |             |

| Entity | Relationship   |
|--------|----------------|
| User   | Friend         |
| User | Complimented   |
| Business | Rate           |
| Review | Activity Wall  |
| Check-In | 

## Review

Review has an unique ID, publish date, and textual content where the content can be text, photo, or a short video. It
has one author and belongs to one business. Also a review has number of stars and number of total votes. Votes can be
categorized as useful and non-useful with a list of users that voted for each of these categories. Moreover, a review
has a list of comments where each comment has an author, textual content, and date.

## Business

A business has an ID, address (street, state, zip code, latitude, longitude), number of reviews, and stars. Also each
business has hours and days of operation. Other attributes of business include parking type (street, garage, lot, or
valet), and ambient type (romantic, classy, touristy, or casual). A business maintains a list of checkin IDs. A review
is belonged to a business.

## Business Category

Each business has one category. Business category has an ID, name, and a list of subcategories. Some categories and
their subcategories are as follow:

- Health & Medical: Dentists, Optometrists, Hospital, Doctors, Physical Therapy, and Allergists
- Restaurants: Bars, Sandwiches, Diners, Burgers, Pizza, Seafood, and Salad
- Hotels & Travel: Bed & Breakfast, Event Planning & Services, and Car Rentals
- Shopping: Flowers & Gifts, Art Supplies, Hardware Stores, Drugstores, Convenience Stores, Department Stores, Home
- Services, Outlet Stores, and Florists
- Food: Bakeries, Coffee & Tea, Grocery, and Food Delivery Services
- Beauty & Spas: Cosmetics & Beauty Supply, and Fashion
- Fitness & Instruction: Active Life, Gyms, Weight Loss Centers, Trainers, Pilates, and Nutritionists
- Education: Colleges & Universities, Middle Schools & High Schools, Adult Schools, Specialty Schools, Dance Studios,
- Preschools, Child Care & Day Care.

You may choose only two of the above categories and their corresponding subcategories for demonstration purposes.

## Photo

A Photo has a unique ID, an author, a description, location, and a list of users who “liked” the photo. Each photo is
either a business photo or a personal photo. A business photo is only visible to a user who checked into that particular
business. A business photo is belonged to a business.

## Check-In

A check-in has an ID and check-in info. A check-in belongs to a business. A user can check-in to a business multiple
times.

Submission Guidelines
You are REQUIRED to submit a pdf to Canvas. It should also include your reasonable assumptions.