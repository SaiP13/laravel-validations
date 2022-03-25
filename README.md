# laravel-validations

use Illuminate\Support\Facades\Validator;<br>
use Validator;

### # USING ARRAY:

        $validatedData = $request->validate([
            'title' => ['required', 'unique:posts', 'max:255'],
            'body' => ['required'],
        ]);
        
### #Normal | :
        $validated = $request->validate([
            'title' => 'required|unique:posts|max:255',
            'body' => 'required',
            'name' => 'unique:posts',
            'start_date' => 'required|date',
            'email' => 'email',
            'size' => 'max:10|min:3',
            'title' => 'size:12', //exactly 12 character long
            'tags' => 'array|size:5', //array size 5
            'image' => 'file|size:512', //exactly 512 kilobytes
            'photo' => 'mimes:jpg,bmp,png', //file types
            'avatar' => 'dimensions:min_width=100,min_height=200',
            'password'=> 'required|confirmed' //match with confirm_password field
        ]);
        
 ### # THIS: 
 
      Automatically control returns back if validate errors occurs
        $this->validate($request, [
            'name' => 'required|unique:users',
            'mobile' => 'required|size:10',
            'email' => 'required|email'
        ]);

### # USING VALIDATOR:

        $validator = Validator::make($request->all(),[
            'name' => 'required',
            'mobile' => 'required',
            'email' => 'required'
        ]);

        if($validator->fails()){
            return response($validator->messages(), 200);
            return response($validator->errors(), 200);
        }
        

### #CUSTOME MESSAGES:
        $validator = Validator::make($request->all(), [
                    'type_id'        => 'required',
                    'seller_id'      => 'required',
                    'name'      => 'required',
                    'product_id'     => 'required',
                ],
                [
                    'type_id.required'   => 'This field cant not be blank',
                    'seller_id.required' => 'seller ID can not be blank',
                    'name.required' => 'Name can not be blank', 
                    'product_id'            => 'Product ID must be enter'
                ]);
### #PRINT ERROR MESSAGES: 
        1) $errors->all()
        2) $errors->get('field_name')
        3) $errors->first('field_name')
        4) $errors->has('email')
        5) @error('email')
        6) $message

### #All:
        @foreach ($errors->all() as $error)
            <li>{{ $error }}</li>
        @endforeach
### #Single error: 
            @error('title')
                <div class="alert alert-danger">{{ $message }}</div>
            @enderror
### #if cond:
            if ($errors->has('email')) {
                {{ $errors->first('email'); || $errors->get('email') }}
            }    
            


    
