# RSpec + Capybara

## Iterate over elements
```
page.all(selector).each do |el|
  some_action
end
```

## Execute single test / test block
Add the `:focus` tag to the test
```
describe 'some kind of test block', :focus do 
  ...
end
```

Run rspec with a the specified tag
```
rspec my_super_cool_test_spec.rb --tag focus
```

## Get value of selected checkbox or radio
```
find_field(selector, checked: true).value
```

## Links
* [Ruby capybara with selenium cheat sheet](https://blog.morizyun.com/blog/capybara-selenium-webdriver-ruby/index.html)
