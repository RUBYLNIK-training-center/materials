## Testing Ruby on Rails code

We'll use RSpec as well for testing Ruby on Rails applications.

In this material, we'll cover 4 different types of tests:

- Model tests
- Controllers tests
- Requests tests
- System tests

---

### Model tests

In models tests, usually you'll find the tests covering the validations and associations.

Consider the following model:

```ruby
class User < ApplicationRecord
  has_many :posts
  
  validates :email, :name, presence: true
end
```

To write a spec for this model you would write something like that:


```ruby
require 'rails_helper'

RSpec.describe User do
  describe 'validations' do
    it 'validates presence of email' do
      user = described_class.new(name: "test user")
      user.valid?

      expect(user.errors).to include("email can't be blank")
    end

    it 'validates presence of name' do
      user = described_class.new(email: "email@email.com")
      user.valid?

      expect(user.errors).to include("name can't be blank")
    end
  end

  describe 'associations' do
    it "has many posts" do
      user = User.create(name: 'name', email: 'email')
      post = Post.create(title: "title", user: user)

      expect(users.posts).to contain_exactly(post)
    end
  end
end

```

Even thou this is a completely valid example, but the testing code itslef is boilerplate. This is why for such obvious tests like validations and associations it's better
to use a helper gem called ["shoulda matchers"](https://github.com/thoughtbot/shoulda-matchers).

It provides a useful set of expectations to test validations and associations easier. E.g.

```ruby
RSpec.describe User, type: :model do
  it { is_expected.to validate_presence_of(:name) }
end
```
---

#### What is my model contains some methods?

If there's more than validations and associations in your model, you should test it like any class, asking yourself a question: what is an input an ouput of the 
function/method I'm testing? Example:

Given there's a User, Post and Like models and we want to have a `#total_likes_received` method in our User model.

```ruby

class User < ApplicationRecord
  has_many :posts
  
  def total_likes_received
    Like.where(post_id: posts.pluck(:id)).count
  end
end
```

A corresponding test would look like this:

```ruby
require 'rails_helper'

RSpec.describe User do
  describe '#total_likes_received' do
    it "returns total likes count on all users's posts" do
      user = User.create(name: 'name', email: 'email')
      post = Post.create(title: "title", user: user)
      like_1 = Like.create(post: post)
      lik2_2 = Like.create(post: post

      expect(users.total_likes_count).to eq 2
    end
  end
end

```

---

### Controller tests



✏️  

---

Please, take your time to carefully read the following materials and do not forget to write your own tests!

#### Links

- 🔗 [2 hour lecture on testing with RSpec from Alexander (RUS)](https://www.youtube.com/watch?v=eVSaLSpHHpY "2 hour lecture on testing with RSpec from Alexander (RUS)") -- the video lecture covers pretty much all the basics you need to get the idea of testing using RSpec.
