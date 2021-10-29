## Testing Ruby on Rails code

We'll use RSpec as well for testing Ruby on Rails applications.

In this material, we'll cover 3 different types of tests:

- Model tests
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

Even thou this is a completely valid example, but the testing code itself is boilerplate. This is why for such obvious tests like validations and associations it's better
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
method I'm testing? Example:

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

### Request tests

Request tests are the integration kind of tests which are aimed to test your app's API. They are smaller then system ones but still very useful since you verify a page (or a API call) works well end-to-end.

Example:

Given you have a Rails API which provides an ability to create users through the `POST /api/users` endpoint.

To test it, you could write something like that:


```ruby
# frozen_string_literal: true

require 'rails_helper'

RSpec.describe 'POST /api/users', type: :request do
  let(:request_uri) { "/api/users" }
  let(:headers) { { 'Authorization' => "Token #{api_key}", 'Host' => 'api.example.com' } }
  let(:api_key) { '1234' }
  let(:params) { { user: user } }

  context 'with valid params' do
    let(:user) do
      {
        email: 'email@email.com',
        password: '1234qwertyuiop',
        forename: 'forename',
        surname: 'surename',
        telephone: '07854 943 728'
      }
    end

    it 'creates a user and returns it' do
      post request_uri, headers: headers, params: params

      expect(status).to be 201
      expect(response_json['forename']).to be_eql user[:forename]
      expect(response_json['errors']).to be_nil
    end
  end

  context 'with invalid params' do
    let(:user) { { email: nil, password: nil, forename: nil, surname: nil, telephone: nil } }

    it 'fails with 422, unprocessable entity' do
      post request_uri, headers: headers, params: params

      expect(status).to be 422
      expect(response_json['errors']).not_to be_empty
    end
  end
end

```

We verify that an API call correctly creates a user and fails if parameters list is invalid.

(!) Since this is an integration test, it does not make sense to test ALL edge cases (remember the material about the testing pyramid). We want to have a balance, so tend to cover all edge cases in your unit tests, whehereas request tests must be used for more high-level checks.



✏️  

---

Please, take your time to carefully read the following materials and do not forget to write your own tests!

#### Links

- 🔗 [2 hour lecture on testing with RSpec from Alexander (RUS)](https://www.youtube.com/watch?v=eVSaLSpHHpY "2 hour lecture on testing with RSpec from Alexander (RUS)") -- the video lecture covers pretty much all the basics you need to get the idea of testing using RSpec.
