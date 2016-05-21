Prepare hw4:

`bundle install --without production`

`rails generate cucumber:install capybara`

`rails generate cucumber_rails_training_wheels:install`

`rails generate rspec:install`

`bundle exec rake db:migrate`

`bundle exec rake cucumber`

`bundle exec rake spec`


To add the director field to the the database and model in rails:

`rails g migration AddDirectorToMovie director:string`

g = generate
AddDirectorToMovie = Add [FieldName] to [TableName/ModelName]
director:string = field name and table type

This generates a migration file in db/migrate, which contains:

```ruby
class AddDirectorToMovie < ActiveRecord::Migration
  def change
      add_column :movies, :director, :string
  end
end
```


Then commit the changes to the schema:

`rake db:migrate`

This will update the db/schema.rb file and add the director field:
```ruby
ActiveRecord::Schema.define(:version => 20130811095234) do

  create_table "movies", :force => true do |t|
      t.string   "title"
      t.string   "rating"
      t.text     "description"
      t.datetime "release_date"
      t.datetime "created_at"
      t.datetime "updated_at"
      t.string   "director"
  end

end
```

To confirm the changes, open the rails console:

`rails console`

```ruby
irb(main):002:0> Movie.columns.map {|c| c.name}
=> ["id", "title", "rating", "description", "release_date", "created_at", "updated_at", "director"]
```

Push the changes out to the test database:

`rake db:test:prepare`
