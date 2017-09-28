Proposed Database Structure:
----------------------------
    Users
     id        | name       | password                | email      | dob        | perms      | account_date
     0001      | kotapie    | :crow:__khav87n86oweru  | g@ex.gg    | 19960618   | 11111111   | 20170923
     0002      | bantyness  | :crow:__7adf74dnfqcfi8  | b@cb.ot    | 19890904   | 10010011   | 20171010
     0003      | roro       | :crow:__m74jd9qnv83nf9  | r@art.st   | 19900205   | 00000011   | 20171128
     ...

id: integer / autoincrement
name: string
password: string
email: string
dob: date
perms: integer / binary
account_date: datetime

    Cards
      id        | name       | set        | number     | type       | hp        | stage       | retreat     | rarity      | dtype       | description | create_date
      1         | Pikachu    | 1          | 24         | 3          | 50        | 1           |             | Promo       |             |             | 20170924
      ...

id: integer / autoincrement
name: string
set: integer (reference to array)
number: integer
type: integer (reference to array)
hp: integer
stage: integer (reference to array)
retreat: integer
rarity: string (validated by array, can also be array reference int)
dtype: integer (reference to type array) (double-type)
description: text

    Cubes
      id        | name       | owner_id   | desc       | has_img    | private   | create_date
      0001      | Poly       | 0001       | cube for c | false      | false     | 20170924
      ...

id: integer / autoincrement
name: string
owner: integer / reference (reference to a user id)
desc: text
has_img: boolean
private: boolean (can be viewed as a guest or by other users)
  / consider int-based privacy settings
create_date: datetime
_HAS MANY COMMENTS_
*Consider*: _BELONGS TO USER_

    Cube_cards
      id        | card_id    | cust_img   | cube_id    | tags       | pimp      | rarity    | side      | add_date
      0001      | 1          |            | 0001       | gray, plc  | 0         | Promo     | false     | 20170924
      ...

id: integer / autoincrement
card_id: integer / reference (reference to a card ID)
image: string (ref to internally stored img)
cube_id: integer / reference (reference to a cube ID) // BELONGS TO CUBE
tags: text (Many to one array, but manageable and comma separable)
pimp: integer (binary set of numbers indicating status)
rarity: string (validated by array, can also be array reference int)
side: boolean
timestamps: datetime
