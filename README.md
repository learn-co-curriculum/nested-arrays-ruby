# Multidimensional Arrays

## Objectives

1. Create nested, or multidimensional, arrays.
2. Read data from a nested array.
3. Write data to a nested array.
4. Iterate over a nested array.

## What is a Nested Array?

An array is like a list but in code form. It is a way for your program to store pieces of data as a collection. Arrays can contain any data types in any combination - strings, integers, even other collections like arrays and hashes.

Arrays are declared by listing variable names or literals separated by commas (`,`) and wrapped in square brackets `[]`. For example:

```ruby
students = ["Mike", "Tim", "Monique"]
```

We know that arrays can contain any type of data, even other arrays. Let's see that in action:

```ruby
nested_students = [
  ["Mike", "Grade 10", "A average"],
  ["Tim", "Grade 10", "C average"],
  ["Monique", "Grade 10", "B Average"]
]
```

A nested, or multidimensional array, is an array whose individual elements are also arrays.

## Why Use a Nested Array?

Nested arrays are useful for storing groups of similar data. One example of nested array usages comes to us from the Google Maps API. Google Maps provides a Javascript function that you, the developer, can use to add Google Maps to your own website. Don't worry about Javascript right now, just understand that a Javascript function is like a Ruby method.

The map-making function (or method, as we're going to think of it) was designed to take in an argument of a nested array - an array in which each index element is an array that contains a place name, latitude and longitude. In other words, something that looks like this:

```ruby
location_array =  [
  ["The Flatiron School", 40.705329, -74.013970],
  ["Disney World", 28.385233, -81.563874]
]
```

## Reading and Writing With Nested Arrays

### Accessing Data From a Nested Array

To access data from and add data to (i.e. "read and write") with a nested array, we can use the same methods we've been using to deal with one-dimensional arrays.

Let's stick with our `students` and `nested_students` arrays for now. To grab an element out of the `students` array, we used bracket notation, plus the index number of the element we want.

```ruby
students = ["Mike", "Tim", "Monique"]
students[0] #=> "Mike"
```

To access the same student's name from our `nested_students` array, we use bracket notation to drill down into the level of the array we want to access.

```ruby
nested_students = [
  ["Mike", "Grade 10", "A average"],
  ["Tim", "Grade 10", "C average"],
  ["Monique", "Grade 11", "B average"]
]

nested_students[0][0] #=> "Mike"
```

The first set of brackets refers to the top-level of the array - the array that contains all of the other arrays.

```ruby
nested_students[0] #=> ["Mike", "Grade 10", "A average"]
```
We can see that the return value of `nested_students[0]` is the element at index 0 of the nested_students array. That element happens to be an array that looks like this:

```ruby
["Mike", "Grade 10", "A average"]
```

If you set the return value of calling `nested_students[0]` equal to a variable, we can then operate on it with further bracket notation:

```ruby
mike = nested_students[0]
mike[0] #=> "Mike"
```

The syntax that we used earlier on: `nested_students[0][0]` is simply the chaining of method calls - we are calling the `[]` method on the return value of calling the `[]` method on `nested_students`.

Let's try that again. This time, let's write a line of code that returns the grade level of the last student in the `nested_students` array. Give it a shot in IRB yourself before reading on.

```ruby
nested_students[2][1] #=> "Grade 11"
```

We are accessing the element at index 2 of the `nested_students` array, which is the last element in that array. That element happens to be an array with three index elements, the second of which (the element at index 1) is the grade level of the student. So, `nested_students[2]` grabs us the array that describes the last student in the list, and chaining on `[1]` grabs the value of the element at index 1 of *that* array - the string `"Grade 11"`.

Now that we are getting comfortable getting data *out* of a nested array, let's work on adding data *to* such an array.

### Adding Data to a Nested Array

To add data to a nested array, we can use the same `<<`, or shovel, method we use to add data to a one-dimensional array.

To add another student to our `students` array:

```ruby
students = ["Mike", "Tim", "Monique"]
students << "Sarah"
students #=> ["Mike", "Tim", "Monique", "Sarah"]
```

To add an element to an array that is nested inside of another array, we use the same bracket notation that we used above to access that nested array, *then* we can use the `<<` on it.

Let's add another piece of info, "Class President" to the nested array that describes Monique.

First, we have to access that particular array, the one that describes our student, Monique.

```ruby
nested_students[2]
```

Then, we can use the `<<`.

```ruby
nested_students[2] << "Class President"
```

Now, our `nested_students` array looks like this:

```ruby
nested_students = [
  ["Mike", "Grade 10", "A average"],
  ["Tim", "Grade 10", "C average"],
  ["Monique", "Grade 11", "B average", "Class President"]
]
```

## Iterating Over Nested Arrays

What if we want to add data to *every array that is nested within the parent array*? It would be very tedious if we had to first calculate the length of the array and then access each individual child array using bracket notation and add to it with the `<<` method, once for each child array.

When we are dealing with a one-dimensional array and we want to do something to every element of the array, we iterate, using methods like `#each ` and `#collect`. If, for example, we wanted to `puts` out every member of the `students` array, we can do so like this:

```ruby
nested_students.each do |student|
  puts student
end
```

In order to manipulate or operate on each element of a nested array, we must iterate down into that level of the array. For example, if you run the following code in IRB:

```ruby
nested_students.each do |student_array|
  print student_array
	puts ""
end
```

You will have outputted:

```ruby
["Mike", "Grade 10", "A average"]
["Tim", "Grade 10", "C average"]
["Monique", "Grade 11", "B average", "Class President"]
```

So, inside the iteration above, we are accessing the list of arrays that make up the top level of the `nested_students` array. If we want to get *inside* of each child array, we continue to iterate, *inside* of the first iteration.

```ruby
nested_students.each do |student_array|
  student_array.each do |student_detail|
    puts student_detail
  end
end
```

Copy and paste the above code into IRB. You should see the following output:

```ruby
Mike
Grade 10
A average
Tim
Grade 10
C average
Monique
Grade 11
B average
Class President
```

## More Nested Arrays

Let's take a look at some multidimensional arrays that have an even deeper nested than the 2D arrays we've just practiced with.

```ruby
very_nested_array = [
  ["this", "is", "the", "first", "child", ["this", "is", "the", "grandchild"]],
  ["now", "we're", "back", "in", "the", "second", "level", ["now", "we're", "back", "in", "the", "grandchild", "level"]]
]
```

In this array we have the top-level, or parent array that contains two children arrays. The array that is the first index element of this parent array contains six elements, the last of which is *yet another array*. The array that is the second index element of the parent array contains eight elements, the last of which is *yet another array*. Here, we have three levels of nesting.

### When to Use a 3D Array

Multidimensional arrays, like the deeply nested one above, are useful for storing hierarchical data. Any collection of information that you can picture like a tree could be a good candidate for a nested array.

Let's take, for example, a music library. You have artists, which each have albums, which in turn have songs. You could picture a structure like this:

![Structure of Data](http://readme-pics.s3.amazonaws.com/Screen%20Shot%202015-09-17%20at%2011.55.01%20AM.png)

And so on, for the various artists in the library. This data structure is considered hierarchical. We could represent it in a nested array that looks something like this:

```ruby
music_library = [["Adele", ["19", ["Day Dreamer", "Best For Last"]], ["21", ["Rollin' In The Deep", "Rumor Has It"]]], ["Beyonce", ["4", ["1 + 1", "Countdown"]], ["Beyonce", ["Haunted", "Pretty Hurts"]]]]
```

When we are working with 3D arrays, it can be difficult to read through the data structure in a way that makes sense. A useful tactic can be formatting the array such that each level of nested is placed on its own line. This can make things much easier to read:

```ruby
music_library = [
  ["Adele",
    ["19",
      ["Day Dreamer", "Best For Last"]
    ],
    ["21",
      ["Rollin' In The Deep", "Rumor Has It"]
    ]
  ],
  ["Beyonce",
    ["4",
      ["1 + 1", "Countdown"]
    ],
    ["Beyonce",
      ["Haunted", "Pretty Hurts"]
    ]
  ]
]
```

Let's try iterating over our `music_library` array.

```ruby
music_library.each do |artist_array|
  artist_array.each do |artist_element|
    # we are inside the first level of the array
    # artist_element = ["Adele", ["19", ["Day Dreamer", "Best For Last"]], ["21", ["Rollin' In The Deep", "Rumor Has It"]]]

    if artist_element.class != Array
      puts "Artist: #{artist_element}"
    else
      artist_element.each do |album_element|
        # we are inside the second level of the array,
        # album_element = ["19", ["Day Dreamer", "Best For Last"]]
        if album_element.class != Array
          puts "Album: #{album_element}"
        else
          album_element.each do |song_element|
            # we are inside the third level of the array
            # song_element = "Day Dreamer"
            puts "Song: #{song_element}"
          end
        end
      end
    end
  end
end
```

We begin by iterating over the first child array, the array that contains all of the information about a particular artist:

```ruby
music_library.each do |artist_array|
  artist_array.each do |artist_element|
    # etc...
  end
end
```

At this level, we are accessing the two child arrays that make up the first tier of the `music_library`. On the first step of, or time through, the iteration, `artist_element` is equal to `["Adele", ["19", ["Day Dreamer", "Best For Last"]], ["21", ["Rollin' In The Deep", "Rumor Has It"]]]`.

We have two checks to put in place if we want to keep iteration. *Some* of the elements of the `artist_element` array are *other arrays*. These need to be iterated over so that we can access what is inside (i.e. information about the albums and songs). But! *Some* of the elements are just strings. *We can't iterate over a string* (you might be thinking). Well, you're absolutely right. Since we can't iterate over a string...we won't! Instead, we'll use `if`/`else` statements to check to see if an element is an array. If it is, we'll iterate over it, if it isn't, we'll simply `put`s it out to the terminal.

```ruby
music_library.each do |artist_array|
  artist_array.each do |artist_element|
    if artist_element.class != Array # check to see if the element is not an array
      puts "Artist: #{artist_element}"
    else # i.e., if the element is an array
      artist_element.each do |album_element|
        # Second level of the iteration
      end
    end
  end
end
```

At the second level of our iteration (where we left off with our `Second level of the iteration` note above), we are operating on the arrays nested *inside* the arrays that describe each artist. On the first step, or time through, the iteration, `album_element` is equal to `["19", ["Day Dreamer", "Best For Last"]]`.

Once again, some of the members of this array are other arrays, some are strings. So, we need to re-use our `if`/`else` logic to determine whether or not we should iterate.

```ruby
# ...
artist_element.each do |album_element|
  if album_element.class != Array
    puts "Album: #{album_element}"
  else
    album_element.each do |song_element|
      # Last level of the iteration
    end
  end
end
# ...
```

Once we are iterating over the `album_element`s that are arrays, we are at the bottom of our `music_library`. There are no more arrays to identify and iterate over. So, all we need to do inside that iteration is `puts` out each `song_element`.

Let's take a look at the whole thing again:

```ruby
music_library.each do |artist_array|
  artist_array.each do |artist_element|
    if artist_element.class != Array
      puts "Artist: #{artist_element}"
    else
      artist_element.each do |album_element|
        if album_element.class != Array
          puts "Album: #{album_element}"
        else
          album_element.each do |song_element|
            puts "Song: #{song_element}"
          end
        end
      end
    end
  end
end
```

Iterating over 3D arrays is tough. Try opening up a new Ruby file in your text editor and writing a method that contains the above code.

### When Not to Use a 3D Array

Three levels deep is about as deep as you want to go when constructing multidimensional arrays. As you can see, things can get messy, fast. If you have more hierarchical data than can fit in a 3D array, it might be better to try using a dictionary-like data structure, called a hash, instead.

<a href='https://learn.co/lessons/nested-arrays-ruby' data-visibility='hidden'>View this lesson on Learn.co</a>

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/nested-arrays-ruby'>Nested Arrays</a> on Learn.co and start learning to code for free.</p>
