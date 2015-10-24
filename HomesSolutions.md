###Exercise: Each

```ruby
homes.each do | home | 
	puts "#{home.name} in #{home.city}"
	puts "Price: #{home.price} a night"
	puts ""
end
```

*Step 1*

First we have begin a new each loop to iterate through each home in our array. Notice we're calling .each on our homes array, and our current element in each iteration is going to be called "home".

*Step 2*

First we use string interpolation to output the current homes name "in" the current home's city with ```home.name``` and ```home.city``` respectively. 

*Step 3*

Then once again through string interpolation we output the current homes price with ```home.price```

*Step 4*

And then one last little trick to end the iteration, we use ``` puts "" ``` to create an empty new line between each home, so they aren't all jammed together. Try removing this line to see what the output looks like.


###Exercise: Map


```ruby
home_price_array = homes.map do | home |
	home.price
end

home_price_total = 0 

home_price_array.each do | home_price |
	home_price_total += home_price
end

average_price = home_price_total / home_price_array.length

puts average_price
```

*Step 1*

First we use a map to iterate over each of our homes, and only return the price into a new array called ```home_price_array```. The key is assigning the result to a variable, our map is going to return a new array, and we need somewhere for it to go.

```ruby
home_price_array = homes.map do | home |
	home.price
end
```

*Step 2*

Then we need to get the total? How do we do this? For now, let's use a .each, with an accumulator called ```home_price_total```.

*Step 3*

Next, we iterate over our new array of home prices, and add the price to our accumulator, home_price_total.

```ruby
home_price_array.each do | home_price |
	home_price_total += home_price
end
```

*Step 4*

Finally we have to calculate our total. This is done by taking our total price of all homes, and dividing it by the length of the array in our home_prices.

```ruby
average_price = home_price_total / home_price_array.length

puts average_price
```

If all goes well, 44 should be output to the screen. 

###Exercise: Reduce

Basically, we're refactoring our previous example into the shorter reduce syntax.

```ruby
homes_price_total = homes.reduce(0.0) do | sum, home | 
	sum + home.price
end

average_price = homes_price_total / homes.length

puts homes_price_total
```

*Step 1*

First we have to create our reduce block. The key with reduce is that we have to assign it to a new variable, just like the map. The difference is that our reduce is not going to necessarily return a new array, it's going to return a new value. 

```ruby
homes_price_total = homes.reduce(0.0) do | sum, home | 
	sum + home.price
end
```

We assign the result of our reduce to a variable called ```homes_price_total```. We call .reduce on our homes array, and give it a starting value of 0.0. 

Then, in our reduce block, we have an accumulator called ```sum```, and just like in the each block our "current home" in the ```home``` variable. 

```ruby
homes_price_total = homes.reduce(0.0) do | sum, home | 
```

We take the homes price attribute, and add it to our sum. 

```ruby
sum + home.price
```

*Step 2*

Finally, we calculate the total like we did before. The value of all of our home's prices is in ```homes_price_total```, then we take that and divide it by the total number of homes from ```homes.length```. 


###Exercise: TextBNB

*Step 1* 

First we have to create an array of homes with different names and values: 

```ruby
homes = [
  Home.new("Nizar's place", "San Juan", 2, 42),
  Home.new("Fernando's place", "Seville", 5, 47),
  Home.new("Josh's place", "Pittsburgh", 3, 41),
  Home.new("Gonzalo's place", "Málaga", 2, 45),
  Home.new("Ariel's place", "San Juan", 4, 49),
  Home.new("Joseph's place", "The Grove", 6, 50),
  Home.new("Lu's Place", "The Gables", 1, 42),
  Home.new("Micah's Place", "Detroit", 2, 40),
  Home.new("Gabe's Place", "Philadelphia", 4, 41),
  Home.new("Tatiana's Place", "New York", 1, 57)
]
```

*Step 2* 

Next up, we can use the exact same each loop we did before to iterate through our list of homes and display them.

```ruby
homes.each do | home | 
	puts "#{home.name} in #{home.city}"
	puts "Price: #{home.price} a night"
	puts ""
end
```

*Step 3*

Then, we have sorting. We can sort by anything in Ruby, as long as we define it, so lets go through some of the ways to tackle this problem.

####*Sort by lowest price*

- First we have to sort the array of homes by price before we display them. We could do something like this: 

  ```ruby
  homes.sort { | home1, home2 | home1.price <=> home2.price }.each do | home | 
  puts "#{home.name} in #{home.city}"
  puts "Price: #{home.price} a night"
  puts ""
  end
  ```

- But that's not a very nice way of doing things. When we start *chaining* array methods our code starts to look ugly. So let's do something different, how about we create a display method to put all of our display logic(our each loop), and just give it homes to display.

	```ruby
	def display(homes)
		homes.each do | home |
			puts "#{home.name} in #{home.city}"
			puts "Price: #{home.price} a night"
			puts ""
		end
	end
	```
		
- Then, we can sort our array and just feed it to the display method. 

	```ruby
		sorted_by_lowest_price = homes.sort do | home1, home2 | 
			home1.price <=> home2.price 
		end

		display(sorted_by_lowest_price)
	```

- Just as with the map, we set our sorted array to a new variable, which is going to be our sorted list. 

- Then we call ```.sort``` on our homes array, and give it two homes ```home1``` and ```home2``` to compare. Remember, we have to compare a specific attribute about the home, since it's an object. So, we pick the home's price.

	```
	home1.price <=> home2.price 
	```

- All in all, it should look like this after we're done: 

	```ruby
	def display(homes)
		homes.each do | home |
			puts "#{home.name} in #{home.city}"
			puts "Price: #{home.price} a night"
			puts ""
		end
	end

	sorted_by_lowest_price = homes.sort do | home1, home2 | 
		home1.price <=> home2.price 
	end

	display(sorted_by_lowest_price)
	```
####*Sort by highest price*

- Sorting by the highest price is exactly like sorting by the lowest price, except with one small change. Let's create an entirely new array of homes sorted by the highest price. 

  ```ruby
  	def display(homes)
  		homes.each do | home |
  			puts "#{home.name} in #{home.city}"
  			puts "Price: #{home.price} a night"
  			puts ""
  		end
  	end

  	sorted_by_lowest_price = homes.sort do | home1, home2 | 
  		home1.price <=> home2.price 
  	end

  	sorted_by_highest_price = homes.sort do | home1, home2 |
  		home2.price <=> home1.price
  	end

  	display(sorted_by_highest_price)
  ```
- Notice anything different here? Obviously we call our ```display``` method with our new array, ```sorted_by_highest_price```, but what else? It's a very small change in our sort block. 
	```
	home2.price <=> home1.price
	```
- We reverse the order in which the home prices are being compared, using Ruby's magic space ship operator, and voila, our array is reversed. 

- Finally we have to get user input to display the homes sorted by what they want: 

	```ruby
	input = ''
	while input != "exit"
		puts "Sort by: price highest / price lowest"
		input = gets.chomp
		if input == "price highest"
			display(sorted_by_highest_price)
		elsif input == "price lowest"
			display(sorted_by_lowest_price)
		elsif input != exit
			puts "I do not recognize that command."
		end
	end
	```
- We create the usual input loop, and then in our conditions we look for a specific input, and then call our display method with the appropriate array. 



####*Sort by Capacity*

- As you can guess, sorting by capacity is very similar to sorting by price. We just need to change one thing.

```ruby
	sorted_by_lowest_capacity = homes.sort do | home1, home2 |
		home1.capacity <=> home2.capacity
	end

	sorted_by_highest_capacity = homes.sort do | home1, home2 |
		home2.capacity <=> home1.capacity
	end
```

- And then we just have to add a couple more conditions to our input's if statement.

```ruby
input = ''
while input != "exit"
	puts "Sort by: price highest / price lowest / capacity highest / capacity lowest"
	input = gets.chomp
	if input == "price highest"
		display(sorted_by_highest_price)
	elsif input == "price lowest"
		display(sorted_by_lowest_price)
	elsif input == "capacity highest"
		display(sorted_by_highest_capacity)
	elsif input == "capacity lowest"
		display(sorted_by_lowest_capacity)
	elsif input != exit
		puts "I do not recognize that command."
	end
end

```

- And there we go, we just call our display method with different sorted arrays depending on what the user inputs.

*Step 4* 

Time to filter by city. 

- Our first step is to get the user's input on what city they want to search for. 

	```ruby
	input = ''
	while input != "exit"
		puts "Select a city: "
		city = gets.chomp
		puts "Sort by: price highest / price lowest / capacity highest / capacity lowest"
		input = gets.chomp
		if input == "price highest"
			display(sorted_by_highest_price)
		elsif input == "price lowest"
			display(sorted_by_lowest_price)
		elsif input == "capacity highest"
			display(sorted_by_highest_capacity)
		elsif input == "capacity lowest"
			display(sorted_by_lowest_capacity)
		else
			puts "I do not recognize that command."
		end
	end
	```
- But then we have to update our display method to actually handle sorting by a city before displaying. How can we do this? 

	```ruby
		[...]
		if input == "price highest"
			display(sorted_by_highest_price, city)
		elsif input == "price lowest"
			display(sorted_by_lowest_price, city)
		elsif input == "capacity highest"
			display(sorted_by_highest_capacity, city)
		elsif input == "capacity lowest"
			display(sorted_by_lowest_capacity, city)
		[...]
	end
	```
- And then we have to update our display method to actually select the city we want from the array.

	```ruby
		def display(homes, city)
			filtered_homes = homes.select do | home |
				home.city == city 
			end

			filtered_homes.each do | home |
				puts "#{home.name} in #{home.city}"
				puts "Price: #{home.price} a night"
				puts ""
			end
		end
	```

	It's important to note that first we use the select method to pick out homes with a city that matches our inputs city. Then, we call our .each on the filtered list of homes, instead of just homes. 



*Step 5*

- Let's create a method to output the average price of all of our homes, and then output it when we use our display method. What are we going to use to calculate the average? None other than reduce. 

	```ruby
	def calculate_average(homes)
		total_price = homes.reduce(0) do | sum, home | 
			sum + home.price
		end
		return total_price / homes.length
	end
	```
	
	Just as before, we created a reduce function that starts at 0, and adds each home's price to the accumulator.

- Now we have to call it from the display method: 

	```ruby
	def display(homes, city)
		filtered_homes = homes.select do | home |
			home.city == city 
		end

		filtered_homes.each do | home |
			puts "#{home.name} in #{home.city}"
			puts "Price: #{home.price} a night"
			puts ""
		end
		puts "The average price of the homes you've selected is: "
		puts calculate_average(filtered_homes)
	end
	```















