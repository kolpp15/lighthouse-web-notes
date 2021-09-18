# W8D5 Notes

## Ruby
- In ruby, "" and '' is different. to use #{}, we must use ""

```ruby
players = ['Lebron', 'Jordan', 'Curry', 'Durrant']

#randomize output
puts players.sample

#shuffle => this will shuffle and output the entire array
puts players.shuffle.inspect #It won't change the original
puts players.shuffle!        #It will change the original array

#------------------------------------------------------------------------

#iteration (everything between do and end can use name)
players.each_with_index do |name, index|
  puts "Hello #{name} at index: ${index}"
end

    #Output:
    `Hello LeBron at index: 0
    Hello Jordan at index: 1
    Hello Curry at index: 2
    Hello Durant at index: 3`

#Other iterators
5.times do |n|
  puts "This is number: ${n}"
end

1.upto() do |n|
  puts "This is number: ${n}"
end
puts

(1..6).each do |n|
  puts "This is number: ${n}"
end

(1..100).step(10) do |n| #This will jump 10s up to 100
  puts "this is number: ${n}"
end

#--------------------------------------------------------------------
def multiples(n)
  output = []

  (1).upto(n) do |n|
    output.push(yield n) # yield will let the second parameter to execute {|n| n * 3}
  end

  return output
end

result =  multiples(5) {|n| n * 3}
puts result.inspect

```

- To access the object:
```ruby
famous_painter = [
  {
    first_name: "Pablo",
    last_name; "Picasso",
    date_of_birth: 1881,
    date_of_death: 1973
  },
  {
    first_name: "Pablo",
    last_name; "Picasso",
    date_of_birth: 1881,
    date_of_death: 1973
  }
]

# This is how to access
puts famous_painter[:last_name]

#This is how to loop
famous_painter.each do [key, val]
  puts "Key: #{key} Value: #{val}"
end

#This is how to loop nested objects
famous_painters.each do |artist|
  artist.each do |key, val|
    puts "Key: #{key} Value: #{val}"
  end
end



```