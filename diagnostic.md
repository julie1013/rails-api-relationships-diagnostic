# Rails API Relationships Diagnostic

Place your responses inside the fenced code-blocks where indivated by comments.

1.  Describe a reason why a join tables may be valuable.

```sh
  # It helps unite two other tables in a many to many relationship. Example:
  # Library patron may have lots of books, and a book may have many library
  # patrons.
```

1.  Provide a database table structure and explain the Entity Relationship that
describes a many-to-many relationship for `Profiles`, `Movies` and `Favorites`
(Think of Netflix). A `Profile` has a `given_name`, `surname` and `email` and a
`Movies` have `title`, `release_date`, and `length` and `Favorites` would be the
join table with references to `Movies` and `Profiles`.

```sh
   CREATE TABLE profiles(
    id SERIAL PRIMARY KEY,
    given_name TEXT,
    surname TEXT,
    email TEXT,
  );

  CREATE TABLE movies(
   id SERIAL PRIMARY KEY,
   title TEXT,
   release_date INTEGER,
   length INTEGER,
 );

  favorites is the table that joins movies and profiles, since movies can
  have many profiles and profiles can have many movies.
```

1.  For the above example, what needs to be added to the Model files?

```rb
class Profile < ActiveRecord::Base
  has_many :movies, through: :favorites
  has_many :favorites, :dependent: :destroy
end
```

```rb
class Movie < ActiveRecord::Base
  has_many :profiles, through: :favorites
  has_many :favorites
end
```

```rb
class Favorite < ActiveRecord::Base
  belongs_to: :profile, inverse_of: :favorites
  belongs_to: :movie, inverse_of: :favorites
end
```

1.  What is the purpose of a serializer? What would our `Profile` serializer look
like to show all movies favorited by a profile on
`http://localhost:3000/profiles/1`

```sh
  # It is to keep certain sensitive information hidden from the client.

```

```rb
class ProfileSerializer < ActiveModel::Serializer
  attributes :id, :favorites
end
```

1.  What would the command be to _scaffold_ out a **join table** for Favorites from
the above `Movies` and `Profiles`.

```sh
  # I know this but I've run out of time!
```

1.  What is `Dependent: Destroy` and where/why would we use it?

```sh
  # It means that favorites, for example, would be dependent on a particular
  #user's profile existing. If the profile is deleted, so are the favorites.
  #No point in having favorites floating around without a person's profile
  #to attach them to!
```

1.  Think of **ANY** example where you would have a one-to-many relationship as well
as a many-to-many relationship in an application. You only need to list the
description about the resources and how they relate to one another.

```sh
  # I know this but I've run out of time!
```
