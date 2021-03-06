# Eloquent Joins

Laravel's Eloquent supports joins, but internally calls the underlying query builder, thereby expecting the name of a table and keys to join it on as arguments. This package allows you to simply call `$model->join($relation)` to join the relationship's table on the keys declared by your relationship, select its columns and hydrate the joined records as models in the resulting collection.

## Installation

Eloquent Joins is installable [with Composer via Packagist](https://packagist.org/packages/tjbp/eloquent-joins).

## Usage

### Use trait

Simply use EloquentJoins\ModelTrait in a model:

```php
namespace App;

use EloquentJoins\ModelTrait as EloquentJoinsModelTrait;

class User
{
    use EloquentJoinsModelTrait;

    protected $table = 'users';

    public function orders()
    {
        return $this->hasMany('\App\Order');
    }
}

$users = User::join('orders')->get();
```

In the above example, `$users` will contain a collection of all the User models with a corresponding Order model (since we've performed an inner join). Each corresponding Order model can be found in the `$orders` property on the User model (normally this would contain a collection of models with a matching foreign key).

You can string multiple `join()` calls, as well as use the other types of join normally available on the underlying query object (`joinWhere()`, `leftJoin()`, etc.).

### Licence

Eloquent Joins is free and gratis software licensed under the [GPL3 licence](https://www.gnu.org/licenses/gpl-3.0). This allows you to use Eloquent Joins for commercial purposes, but any derivative works (adaptations to the code) must also be released under the same licence. Mustard is built upon the [Laravel framework](http://laravel.com), which is licensed under the [MIT licence](http://opensource.org/licenses/MIT).
