# Dslh

It define Hash as a DSL.

[![Gem Version](https://badge.fury.io/rb/dslh.png?201403101612)](http://badge.fury.io/rb/dslh)
[![Build Status](https://drone.io/github.com/winebarrel/dslh/status.png?201403101612)](https://drone.io/github.com/winebarrel/dslh/latest)

## Installation

Add this line to your application's Gemfile:

    gem 'dslh'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install dslh

## Usage

```ruby
require 'dslh'
require 'pp'

h = Dslh.eval do
  glossary do
    title "example glossary"
    GlossDiv do
      title "S"
      GlossList do
        GlossEntry do
          ID "SGML"
          SortAs "SGML"
          GlossTerm "Standard Generalized Markup Language"
          Acronym "SGML"
          Abbrev "ISO 8879:1986"
          GlossDef do
            para "A meta-markup language, used to create markup languages such as DocBook."
            GlossSeeAlso "GML", "XML"
          end
          GlossSee "markup"
        end
      end
    end
  end
end

# It can also evaluate string:
# ---
# Dslh.eval(<<-EOS, :filename => 'my.rb', :lineno => 100)
#   foo 'bar'
#   zoo do
#     baz 100
#   end
# EOS

pp h
```

```ruby
# h =>
{:glossary=>
  {:title=>"example glossary",
   :GlossDiv=>
    {:title=>"S",
     :GlossList=>
      {:GlossEntry=>
        {:ID=>"SGML",
         :SortAs=>"SGML",
         :GlossTerm=>"Standard Generalized Markup Language",
         :Acronym=>"SGML",
         :Abbrev=>"ISO 8879:1986",
         :GlossDef=>
          {:para=>
            "A meta-markup language, used to create markup languages such as DocBook.",
           :GlossSeeAlso=>["GML", "XML"]},
         :GlossSee=>"markup"}}}}}
```

### deval

```ruby
require 'dslh'

h = {"glossary"=>
      {"title"=>"example glossary",
       "GlossDiv"=>
        {"title"=>"S",
         "GlossList"=>
          {"GlossEntry"=>
            {"ID"=>"SGML",
             "SortAs"=>"SGML",
             "GlossTerm"=>"Standard Generalized Markup Language",
             "Acronym"=>"SGML",
             "Abbrev"=>"ISO 8879:1986",
             "GlossDef"=>
              {"para"=>
                "A meta-markup language, used to create markup languages such as DocBook.",
               "GlossSeeAlso"=>["GML", "XML"]},
             "GlossSee"=>"markup"}}}}}

puts Dslh.deval(h) # => glossary do
                   #      title "example glossary"
                   #      GlossDiv do
                   #        title "S"
                   #        GlossList do
                   #          GlossEntry do
                   #            ID "SGML"
                   #            SortAs "SGML"
                   #            GlossTerm "Standard Generalized Markup Language"
                   #            Acronym "SGML"
                   #            Abbrev "ISO 8879:1986"
                   #            GlossDef do
                   #              para "A meta-markup language, used to create markup languages such as DocBook."
                   #              GlossSeeAlso "GML", "XML"
                   #            end
                   #            GlossSee "markup"
                   #          end
                   #        end
                   #      end
                   #    end
```

## Contributing

1. Fork it ( http://github.com/<my-github-username>/dslh/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
