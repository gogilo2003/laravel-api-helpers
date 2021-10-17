# Api Response Helpers
Laravel Api Response Helpers for consistent response in laravel REST apis

## Installation
Add repositories to composer.json
```
"repositories": [
    {
        "type": "vcs",
        "url": "https://github.com/gogilo2003/laravel-api-response-helpers"
    }
]
    
```
Run composer require
```
composer require gogilo/laravel-api-response-helpers
```

Use this trait in with your api controller

## Example
```
class UserController extends Controller
{
    use Ogilo\ApiResponseHelper;

    public function store(Request $request){
        $validator = Validator::make($request->all(),[
            'name'=>'required',
            'email'=>'required|email|unique:users,email',
            'password'=>'required|min:6',
        ]);

        if($validator->fails()){
            return $this->validationError($validator);
        }

        $user = new User();
        $user->name = $request->name;
        $user->email = $request->email;
        $user->password = bcrypt($request->password);
        $user->save();

        return $this->storeSuccess('User Created',['user'=>$user]);
    }
}
```

## Methods
```
$this->validationError($validator)
   
$this->storeSuccess($message, $data = [])

$this->updateSuccess($message, $data = [])

$this->deleteSuccess()

$this->importSuccess($message, $data = [])
```

---
Feel free to leave comments for improvement
