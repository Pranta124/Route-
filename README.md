# Route-
# Route
``
<?php

use Illuminate\Support\Facades\Route;
use App\Http\Controllers\UserController;

use App\Http\Controllers\TaskController;
/*
|--------------------------------------------------------------------------
| Web Routes
|--------------------------------------------------------------------------
|
| Here is where you can register web routes for your application. These
| routes are loaded by the RouteServiceProvider within a group which
| contains the "web" middleware group. Now create something great!
|
*/

Route::get('/', function () {
    return view('welcome');
});
Route::get('/gretting',function()
{
    return 'Hello world';
});
Route::get('/Pranta',function(){
 return "pranta";
});
// Route::view('/welcome','Welcome');
Route::view('/welcome','welcome',['name'=>'pranta']);
Route::get('/user/{id}',[UserController::class,'show'])->name('pranta');
Route::get('/user/{id}',[UserController::class,'edit']);
Route::get('/user/{id}',function($id){
    return 'User'.$id;
});
Route::get('/user/{id}',function($id)
{
    return 'Prema'.$id;
});
//tasks
Route::resource('task',TaskController::class)->except(['destroy']);
Route::group(['middleware'=>'auth'],function(){
    Route::group([ 
        'middleware'=>'user',
        'prefix'=>'user',
        'as'=>'user.'
        ],function(){
         Route::resource('task',TaskController::class);
         Route::resource('projects',ProjectController::class);
    });
    Route::group([
        'middleware'=>'admin',
        'prefix'=>'admin',
        'as'=>'admin.'
    ],function(){
    Route::resource('user',UserController::class);
});
}); 

``
