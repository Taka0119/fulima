# fulima Database設計

## users
|Column|Type|Option|
|------|----|------|
|name|string|null: false|
|email|string|null: false, unique: true|
|password|string|null: false|
|family_name|string|null: false|
|first_name|string|null: false|
|family_name_kana|string|null: false|
|first_name_kane|string|null: false|
|birthday|date|null: false|
|icon|string||
### Association
- belongs_to :shipment
- belongs_to :sns_authentication
- belongs_to :creditcard
- has_many :items
- has_many :orders
- has_many :likes
- has_meny :like_items, through: :likes, source: :item
- has_many :comments
- has_many :infomations
- has_many :todo_lists
- has_many :buyer_user_evaluations, class_name: 'User_evaluation', foreign_key => 'buyer_id' <!-- user_evaluationのbuyer_idを参照 -->
- has_many :seller_user_evaluations, class_name: 'User_evaluation', foreign_key => 'seller_id' <!-- user_evaluationのseller_id参照 -->

## shipments
|Column|Type|Option|
|------|----|------|
|family_name|string|null: false|
|first_name|string|null: false|
|family_name_kana|string|null: false|
|first_name_kana|string|null: false|
|postal_code|string|null: false|
|prefectures|string|null: false|
|city|string|null: false|
|address|string|null: false|
|mansion_name|string||
|room_number|string||
|phone_number|string||
|user_id|integer|null: false, foreign_key: true|
### Association
- has_many :users

## items
|Column|Type|Option|
|------|----|------|
|name|string|null: false|
|description|text|null: false|
|category_id|integer|null: false|
|size|string||
|brand_id|integer|foreign_key: true|
|status_id|integer|null: false, foreign_key: true|
|delivery_fee_id|integer|null: false, foreign_key: true|
|shipping_method_id|integer|null: false, foreign_key: true|
|prefecture|string|null: false|
|date_of_ship_id|integer|null: false, foreign_key: true|
|price|integer|null: false|
|user_id|integer|null: false, foreign_key: true|
|sold_out|boolean|null: false|
### Association
- belongs_to :user
- belongs_to :status
- belongs_to :delivery_fee
- belongs_to :shipping_method
- belongs_to :date_of_ship
- belongs_to :category
- belongs_to :brand
- belongs_to :user_evaluations
- has_many :images
- has_many :orders
- has_many :likes
- has_many :like_users, through: :likes, source: :user
- has_many :comments


## images
|Column|Type|Option|
|------|----|------|
|image|string|null: false|
|item_id|integer|null: false, foreign_key: true|
### Association
- belongs_to :item

## brands
|Column|Type|Option|
|------|----|------|
|name|string|null: false|
|item_id|integer|null: false, foreign_key: true|
### Association
- has_many :items

## categories
|Column|Type|Option|
|------|----|------|
|name|string|null: false|
|ancentry||null: false|
### Association
- has_many :items

## statuses
|Column|Type|Option|
|------|----|------|
|status|string|null: false|
|item_id|integer|null: false, foreign_key: true|
### Association
- has_many :items

## delivery_fees
|Column|Type|Option|
|------|----|------|
|delivery_fee|string|null: false|
|item_id|integer|null: false, foreign_key: true|
### Association
- has_many :items

## shipping_methods
|Column|Type|Option|
|------|----|------|
|shipping_method|string|null: false|
|item_id|integer|null: false, foreign_key:true|
### Association
- has_many :items

## date_of_ships
|Column|Type|Option|
|------|----|------|
|date_of_ship|string|null: false|
|item_id|integer|null: false, foreign_key: true|
### Association
- has_many :items

## orders_user_item
|Column|Type|Option|
|------|----|------|
|number|integer|null: false|
|item_id|integer|null: false, foreign_key: true|
|user_id|integer|null: false, foreign_key: true|
### Association
- belongs_to :item
- belongs_to :user

## user_evaluations
|Column|Type|Option|
|------|----|------|
|review|text|null: false|
|evaluation_id|integer|null: false, foreign_key: true|
|buyer_id|integer|null: false, foreign_key: true| <!-- userの商品購入者ID user_idが入る -->
|seller_id|integer|null: false, foreign_key: true| <!-- userの商品出品者ID user_idが入る -->
### Association
- belongs_to :evaluation
- belongs_to :buyer, class_name: 'User' :foreign_key => 'buyer_id' 
- belongs_to :seller, class_name: 'User' :foreign_key => 'seller_id'

## evaluations
|Column|Type|Option|
|------|----|------|
|evaluation|string|null: false|
|user_evaluation_id|integer|null: false, foreign_key: true|
### Association
- has_many :user_evaluations

## likes
|Column|Type|Option|
|------|----|------|
|user_id|integer|null: false, foreign_key: true|
|item_id|integer|null: false, foreign_key: true|
### Association
- belongs_to :user
- belongs_to :item

## comments
|Column|Type|Option|
|------|----|------|
|comment|text|null: false|
|user_id|integer|null: false, foreign_key: true|
|item_id|integer|null: false, foreign_key: true|
### Association
- belongs_to :user
- belongs_to :item

## creditcards
|Column|Type|Option|
|------|----|------|
|user_id|integer|null: false, foreign_key: true|
|customer_id|integer|null: false, foregin_key: true|
|catd_id|integer|null: false, foreign_key: true|
|date|timestamps|null: false|
### Association
- belongs_to :user

## infomations
|Column|Type|Option|
|------|----|------|
|titile|string|null: false|
|content|text|null: false|
|user_id|integer|null: false|
### Association
- belongs_to :user

## todo_lists
|Column|Type|Option|
|------|----|------|
|list|string|null: false|
|user_id|integer|null: false, foreign_key: true|
### Association
- belongs_to :user