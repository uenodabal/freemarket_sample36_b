# README

## usersテーブル
|Column|Type|Options|
|------|----|-------|
|nickname|string|null: false|
|email|string|null: false, unique: true|
|family-name|string|null: false|
|first-name|string|null: false|
|kana-family-name|string|null: false|
|kana-first-name|string|null: false|
|birth_year|integer|null: false|
|birth_month|integer|null: false|
|birth_day|integer|null: false|
|credit|integer|null: false, unique: true|
|tel|string||
|adress|string||
|profil-image|string||
|profil-comment|text||

### Association
- has_many :items
- has_many :comments
- has_many :reviews
- has_many :likes
- has_many :adressees
- has_many :points
- has_many :procceeds
- has_many :statuses


## itemsテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
|introduce|text|null: false|
|price|integer|null: false|
|seller_id|integer|null: false|

### Association
- has_many :comments
- has_many :item_images
- has_many :category, through: item_categories
- has_many :item_categories
- belongs_to :user
- belongs_to :status
- belongs_to :evalution
- belongs_to :good
- belongs_to :area
- belongs_to :brand
- belongs_to :fee
- belongs_to :sipping_method


## statusesテーブル
|Column|Type|Options|
|------|----|-------|
|stage|integer|null: false|
|buyer_id|references|null: false, unique: true|

### Association
- has_many :users
- has_many :items
- has_many :comments


## categoriesテーブル
|Column|Type|Options|
|------|----|-------|
|id|integer|null: false|
|category|string|null: false|
|parent_id|integer||

### Association
- has_many :items, through: item_categories
- has_many :item_categories


## item_categoriesテーブル
|Column|Type|Option|
|------|----|------|
|item_id|references|null: false, foreing_key: true|
|category_id|references|null; false, foreing_key: true|

### Association
- belongs_to :category, through: :item_categories
- belongs_to :item_categories


## brandsテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false|

### Association
has_many :brand_group, through: :brand_brand-group
has_many :brand_brand-group


## brand_brand-groupsテーブル
|Column|Type|Options|
|------|----|-------|
|brand_id|references|null: false, foreing_key: true|
|brand-group_id|references|null: false, foreing_key: true|

### Association
belogns_to :brand
belongs_to :brand_group


## brand-groupsテーブル
|Column|Type|Options|
|------|----|-------|
|brand-group|string|null: false|

### Association
has_many :brands, through: :brand-categories
has_many :brands-categories


## commentsテーブル
|Column|Type|Options|
|------|----|-------|
|comment|text|null: false|
|user_id|references|null: false|
|item_id|references|null: false|
|status_id|references|null: false|

### Association
- belongs_to :user
- belongs_to :item
- belongs_to :status


## reviewsテーブル
|Column|Type|Options|
|------|----|-------|
|review|string|null: false|
|comment|text|null: false|
|user_id|references|null: false|
|item_id|references|null: false|

### Association
- belongs_to :user
- belongs_to :item


## likesテーブル
|Column|Type|Options|
|------|----|-------|
|like|boolean|null: false|
|user_id|references|null: false, foreing_key: true|
|item_id|references|null: false, foreing_key: true|

### Association
belongs_to :users
belongs_to :items


## adresseeテーブル
|Column|Type|Options|
|------|----|-------|
|postal-code|string|null: false|
|prefecture|string|null :false|
|city|string|null: false|
|block_number|integer|null: false|
|bilding_name|string||
|tel|string||
|user_id|references|null: false|

### Association
has_one :user


## areasテーブル
|Column|Type|Options|
|------|----|-------|
|area|string|null: false|
|parent_id|integer||                      ＊＊＊　必要？
|adressee_id||                            ＊＊＊　必要？
|item_id|references|null: false|

### Association
has_many :items


## Freight-payersテーブル
|Column|Type|Options|
|------|----|-------|
|payer|string|null: false|

### Association
has_many :items
has_many :freight_methods
has_many :shipping-methond_id, through: :freight-methods



## freight_methodsテーブル
|Column|Type|Options|
|------|----|-------|
|freight-payer_id|references|null: false, unique: true|
|shipping-method_id|references|null: false, uniquie: true|

### Associtation
belongs_to :freight_payer
belongs_to :shipping_method



## shipping-methodsテーブル
|Column|Type|Options|
|------|----|-------|
|method|string|null: false|

### Association
has_many :items
has_many :freight_methods
has_many :freight-payers, through: :freight_method



## item-imagesテーブル
|Column|Type|Options|
|------|----|-------|
|image|string|null: false|
|item_id|references|null: false|

### Association
belongs_to :items


## pointsテーブル
|Column|Type|Options|
|------|----|-------|
|points|integer|null:false|
|user_id|references|null: false|

### Association
belongs_to :user


## proceedsテーブル
|Column|Type|Options|
|------|----|-------|
|proceeds|integer|null: false|
|user_id|references|null: false|

### Association
belongs_to :user
