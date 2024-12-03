---
layout: post
title:  "Word Frequency"
date:   2024-12-03 14:30:24 +0700
categories: jekyll update
---
Here’s a useful Ruby code for generating a hash with default values while dynamically counting occurrences of items in an array.

```ruby
def word_frequency(sentence)
  frequency = Hash.new(0) # Default value is 0

  sentence.split.each do |word|
    clean_word = word.downcase.gsub(/[^a-z0-9]/i, '') # Remove punctuation
    frequency[clean_word] += 1
  end

  frequency
end

# Example Usage
sentence = "Ruby is amazing! Ruby is fast, Ruby is fun."
puts word_frequency(sentence)
# Output:
# {"ruby"=>3, "is"=>3, "amazing"=>1, "fast"=>1, "fun"=>1}
```
