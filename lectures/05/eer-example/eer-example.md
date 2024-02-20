---
title: (E)ER-Exmaple
---

# Design Specification

The following is a description of the information required for a database system
that processes information about PhotoSmart, an online photo sharing website
provides users with different functionalities and features.
The database must represent the following information:  


## Photo Information

- A photo is identified by a photo ID.
  - **STRONG ENTITY PRIMARY KEY: photo_id**
- Every photo is published by a user.
  - **ENTITY: User** 
  - **RELATIONSHIP: Publish**
  - **PARTICIPATION: Total 1:N Partial**
- Photos can belong to sets. Each set can have one or more than one photos (- It’s not mandatory for each photo to belong to a set. Some photos can belong to more than one set).
  - **ENTITY: Photo** 
  - **RELATIONSHIP: Belongs**
  - **PARTICIPATION: Total M:N Partial**
- Each Photo has information about the time and location it was taken.
  - ATTRIBUTE (simple, single-valued, stored): Time
  - ATTRIBUTE (composite, single-valued, stored): location
    - ATTRIBUTE (simple, single-valued, stored): x
    - ATTRIBUTE (simple, single-valued, stored): y
- Each photo can have several tags (keywords describing the photo).
  - ATTRIBUTE (simple, multivalued, stored): tags
- Each photo is taken by a camera.
  - ENTITY: Camera
  - RELATIONSHIP: Capture
  - PARTICIPATION: Total 1:N Partial
- Each photo belongs to a certain category (e.g., a photo can be in the category of portrait, art or screenshot.
  - ATTRIBUTE (simple, single-valued, stored): category
- Moreover, the privacy level of a photo can be either private or public.
  - ATTRIBUTE (simple, single-valued, stored): privacy-level-photo
- A description is also assigned to each photo.
  - ATTRIBUTE (simple, single-valued, stored): Description

## User Information

- Every user has a unique screen name (id).
  - **STRONG ENTITY PRIMARY KEY: photo_id**
- Each user also has a name, date of birth and age which is computed from his date of birth.
  - ATTRIBUTE (simple, single-valued, stored): name
  - ATTRIBUTE (simple, single-valued, stored): DOB
  - ATTRIBUTE (simple, single-valued, derived[DOB]): age
- He also has contact information which includes his email and phone number.
  - ATTRIBUTE (composite, single-valued, stored): contact
    - ATTRIBUTE (simple, single-valued, stored): email
    - ATTRIBUTE (simple, single-valued, stored): phone
- Users can be either guests or members.
  - CONSTRAINT: Disjoint Set
    - ENTITY: Guest
      - PARTICIPATION: TOTAL M:N PARTIAL
      - Guest has an expiration date.
        - ATTRIBUTE (simple, single-valued, stored): exp. date
    - ENTITY: Member
      - PARTICIPATION: TOTAL M:N PARTIAL
      - Members can be either basic members or pro members.
        - CONSTRAINT: Disjoint Set
          - ENTITY: Basic
          - PARTICIPATION: TOTAL M:N PARTIAL
            - Basic users have two limitations: number of photos they can upload and amount of disk they can use.
              - ATTRIBUTE (simple, single-valued, stored): Max # of photos
              - ATTRIBUTE (simple, single-valued, stored): Max space
          - ENTITY: Pro
          - PARTICIPATION: TOTAL M:N PARTIAL
            - Pro members have an annual membership fee.
              - ATTRIBUTE (simple, single-valued, stored): Annual fee
- Users can be friend of other users.
  - **ENTITY: User** 
  - **RELATIONSHIP: Friend**
  - **PARTICIPATION: Partial M:N Partial**
- Users can comment on as many photos as they want.
  - **ENTITY: Photo** 
  - **RELATIONSHIP: Comment**
  - **PARTICIPATION: Partial M:N Partial**
    - Each comment has a description and time.
      - ATTRIBUTE (simple, single-valued, stored): time
      - ATTRIBUTE (simple, single-valued, stored): desc
- Users can make any photo as their favorite (they can have 0,1 or more favorite photos) as long as the privacy level of the photo is public.
  - **ENTITY: Photo** 
  - **RELATIONSHIP: Favorite**
  - **PARTICIPATION: Partial M:N Partial**
- Users surf PhotoSmart in several (0,1 or more) sessions.
  - **ENTITY: Session** 
  - **RELATIONSHIP: Surf**
  - **PARTICIPATION: Partial 1:N Total**


## Camera Information

- Cameras are identified by a unique identifier (camera id).
  - **STRONG ENTITY PRIMARY KEY: photo_id**
- Cameras also have brand name and model number.
  - ATTRIBUTE (simple, single-valued, stored): brand
  - ATTRIBUTE (simple, single-valued, stored): model

## Set Information

- Each set has a creation date and description.
  - ATTRIBUTE (simple, single-valued, stored): creation date
  - ATTRIBUTE (simple, single-valued, stored): description
- Each set also has a privacy level (either public or private).
  - ATTRIBUTE (simple, single-valued, stored): set-privacy-level

## Session Information
- The session-id is unique for a given user but it may be redundant across several users.
  - **WEAK ENTITY PRIMARY KEY: photo_id**
- A session has a session-id, a start date/time, an end date/time, and a duration which is computed from start and end time.
  - ATTRIBUTE (simple, single-valued, stored): s_time
  - ATTRIBUTE (simple, single-valued, stored): e_time
  - ATTRIBUTE (simple, single-valued, derived[e_time - s_time]): duration
- Each session includes a reference to one user in the system.
