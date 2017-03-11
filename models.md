# Models

For now, the only thing I know here is that we can validate the attributes.

```ruby
class Micropost < ApplicationRecord
  validates :content, length: { maximum: 140 }
end
```

Turns out you can also set up Entity Relationships (or, in Rails speak, *associations*):

```ruby
class User < ApplicationRecord
  has_many :microposts
end

class Micropost < ApplicationRecord
  belongs_to :user
  validates :content, lenght: {maximum: 140 }
end
```
