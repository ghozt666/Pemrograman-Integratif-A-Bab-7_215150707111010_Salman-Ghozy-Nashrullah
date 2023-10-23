# Pemrograman-Integratif-A-Bab-7_215150707111010_Salman-Ghozy-Nashrullah

<h1>Langkah Percobaan</h1>
<h2>Pembuatan tabel</h2>
<p>Berikut adalah tabel yang akan digunakan pada percobaan ini</p>
 <table border="1">
        <tr>
            <td>posts</td>
            <td>id</td>
            <td>content(STRING)</td>
        </tr>
        <tr>
            <td>comments</td>
            <td>id</td>
            <td>review(STRING)</td>
        </tr>
        <tr>
            <td>tags</td>
            <td>id</td>
            <td>name</td>
        </tr>
        <tr>
            <td>post_tag</td>
            <td>postId</td>
            <td>tagId</td>
        </tr>
    </table>
<h3>Langkah ke-1</h3>
<p>1. Sebelum membuat migrasi <i>database</i> atau membuat tabel pastikan <i>server database</i>
aktif kemudian pastikan sudah membuat <i>database</i> dengan nama <i>lumenpost</i></p>
<img src="gambar/100.PNG">

<h3>Langkah ke-2</h3>
<p>2. Kemudian ubah konfigurasi<i> database pada <i>file .env</i> menjadi seperti berikut</p>
<i>
DB_CONNECTION=mysql
<br>
DB_HOST=127.0.0.1
<br>
DB_PORT=3306
<br>
DB_DATABASE=lumenpost
<br>
DB_USERNAME=root
</i>
<i>
DB_PASSWORD=</i>
<br><br>
<img src="gambar/1.PNG">

<h3>Langkah ke-3</h3>
<p>3. Setelah mengubah konfigurasi pada <i>file .env</i>, kita juga perlu menghidupkan
beberapa <i> library</i> bawaan dari <i>lumen</i> dengan membuka <i>file app.php</i> pada <i>folder
bootstrap</i> dan mengubah baris ini </p>
<i>
// $app->withFacades();<br>
// $app->withEloquent();</i> <br><br>

<p> menjadi</p>

<i>$app->withFacades();<i><br>
</i> $app->withEloquent(); </i>

<img src = "gambar/2.PNG">

<h3>Langkah ke-4</h3>
<p>4. Setelah itu jalankan <i>command</i> berikut untuk membuat <i>file migration</i></p>
<i>php artisan make:migration create_posts_table<br>
php artisan make:migration create_comments_table<br>
php artisan make:migration create_tags_table<br>
php artisan make:migration create_post_tag_table<br>
</i><br><br>
<img src = "gambar/3.PNG">

<h3>langkah ke-5</h3>
<p>5. Ubah fungsi <i>up()</i> pada <i>file migrasi create_posts_table</i></p>
#sebelumnya
<br>...
<br>public function up()
<br>{
<br>Schema::create('posts', function (Blueprint $table) {
<br>$table->id();
<br>$table->timestamps();
<br>});
<br>}
<br>...

<br>#diubah menjadi
<br>...
<br>public function up()
<br>{
<br>Schema::create('posts', function (Blueprint $table) {
<br>$table->id();
<br>$table->timestamps();
<br>$table->string('content');
<br>});
<br>}
<br>...

<img src = "gambar/4.PNG">

<h3>langkah ke-6</h3>
<p>5. Ubah fungsi <i>up()</i> pada <i>file create_comments_table</i></p>
#sebelumnya
<br>...
<br>public function up()
<br>{
<br>Schema::create('posts', function (Blueprint $table) {
<br>$table->id();
<br>$table->timestamps();
<br>});
<br>}
<br>...

<br>#diubah menjadi
<br>...
<br>public function up()
<br>{
<br>Schema::create('posts', function (Blueprint $table) {
<br>$table->id();
<br>$table->timestamps();
<br>$table->string('review');
<br>$table->foreignId('postId')->unsigned();
<br>});
<br>}
<br>...

<img src = "gambar/5.PNG">

<h3>langkah ke-7</h3>
<p>5. Ubah fungsi <i>up()</i> pada <i>file create_tags_table</i></p>
#sebelumnya
<br>...
<br>public function up()
<br>{
<br>Schema::create('posts', function (Blueprint $table) {
<br>$table->id();
<br>$table->timestamps();
<br>});
<br>}
<br>...

<br>#diubah menjadi
<br>...
<br>public function up()
<br>{
<br>Schema::create('posts', function (Blueprint $table) {
<br>$table->id();
<br>$table->timestamps();
<br>$table->string('name');
<br>});
<br>}
<br>...

<img src = "gambar/6.PNG">

<h3>langkah ke-8</h3>
<p>5. Ubah fungsi <i>up()</i> pada <i>file migrasi create_post_tag_table</i></p>
#sebelumnya
<br>...
<br>public function up()
<br>{
<br>Schema::create('posts', function (Blueprint $table) {
<br>$table->id();
<br>$table->timestamps();
<br>});
<br>}
<br>...

<br>#diubah menjadi
<br>...
<br>public function up()
<br>{
<br>Schema::create('posts', function (Blueprint $table) {
<br>$table->id();
<br>$table->timestamps();
<br>$table->foreignId('postId')->unsigned();
<br>$table->foreignId('tagId')->unsigned();
<br>});
<br>}
<br>...

<img src = "gambar/7.PNG">

<h3>langkah ke-9</h3>
<p>9. Kemudian jalankan <i>command</i></p>
<i>php artisan migrate</i><br><br>
<img src="gambar/8.PNG">

<h2>Pembuatan Model</h2>
<h3>langkah ke-1</h3>
<p>1. Buatlah <i>file</i> dengan nama <i>Post.php</i> dan isi dengan baris kode berikut</p>
<i><?php
<br>namespace App\Models;
<br>use Illuminate\Database\Eloquent\Model;
<br>class Post extends Model
<br>{
<br>/**
<br>* The attributes that are mass assignable.
<br>*
<br>* @var string[]
<br>*/
<br>protected $fillable = [
<br>'content'
<br>];
<br>/**
<br>* The attributes excluded from the model's JSON form.
<br>*
<br>* @var string[]
<br>*/
<br>protected $hidden = [];
<br>}</i><br><br>
<img src="gambar/9.PNG">

<h3>langkah ke-2</h3>
<p>2. Buatlah <i>file</i> dengan nama <i>Comment.php</i> dan isi dengan baris kode berikut</p>
<i>
<br><?php
<br>namespace App\Models;
<br>use Illuminate\Database\Eloquent\Model;
<br>class Comment extends Model
<br>{
<br>/**
<br>* The attributes that are mass assignable.
<br>*
<br>* @var string[]
<br>*/
<br>protected $fillable = [
<br>'review'
<br>];
<br>/**

<br>* The attributes excluded from the model's JSON form.
<br>*
<br>* @var string[]
<br>*/
<br>protected $hidden = [];
<br>}<br><br>

<img src="gambar/10.PNG">

<h3>langkah ke-3</h3>
<p>2. Buatlah <i>file</i> dengan nama <i>Tag.php</i> dan isi dengan baris kode berikut</p>
<i>
<br><?php
<br>namespace App\Models;
<br>use Illuminate\Database\Eloquent\Model;
<br>class Tag extends Model
<br>{
<br>/**
<br>* The attributes that are mass assignable.
<br>*
<br>* @var string[]
<br>*/
<br>protected $fillable = [
<br>'review'
<br>];
<br>/**

<br>* The attributes excluded from the model's JSON form.
<br>*
<br>* @var string[]
<br>*/
<br>protected $hidden = [];
<br>}<br><br>

<img src="gambar/11.PNG">

<h2>Relasi One-to-Many</h2>
<h3>langkah ke-1</h3>
<p>1. Tambahkan fungsi <i>comments()</i> pada <i>file Post.php</i></p>
<i><br><?php
<br>namespace App\Models;
<br>use Illuminate\Database\Eloquent\Model;
<br>class Post extends Model
<br>{
<br>...


<br>// fungsi comments
<br>public function comments()
<br>{
<br>return $this->hasMany(Comment::class, 'postId');
<br>}
<br>}<br><br>
<img src="gambar/12.PNG">

<h3>langkah ke-2</h3>
<p>1. Tambahkan fungsi <i>post()</i> dan atribut <i>postId</i> pada <i>file Comment.php</i></p>

<i><?php
<br>namespace App\Models;
<br>use Illuminate\Database\Eloquent\Model;
<br>class Comment extends Model
<br>{
<br>...
<br>protected $fillable = [
<br>'review',
<br>'postId' // atribut postId
<br>];
<br>/**
<br>* The attributes excluded from the model's JSON form.
<br>*
<br>* @var string[]
<br>*/
<br>protected $hidden = [];
<br>public function post()
<br>{
<br>return $this->belongsTo(Post::class, 'postId');
<br>}
<br>}</i><br><br>
<img src="gambar/13.PNG">

<h3>langkah ke-3</h3>
<p>3. Buatlah <i>file PostController.php</i> dan isilah dengan baris kode berikut</p>
<i><?php
<br>namespace App\Http\Controllers;
<br>use App\Models\Post;
<br>use Illuminate\Http\Request;
<br>class PostController extends Controller

<br>{
<br>/**
<br>* Create a new controller instance.
<br>*
<br>* @return void
<br>*/
<br>public function __construct()
<br>{
<br>//
<br>}
<br>//
<br>public function createPost(Request $request)
<br>{
<br>$post = Post::create([
<br>'content' => $request->content,
<br>]);
<br>return response()->json([
<br>'success' => true,
<br>'message' => 'New post created',
<br>'data' => [
<br>'post' => $post
<br>]
<br>]);
<br>}
<br>public function getPostById(Request $request)
<br>{
<br>$post = Post::find($request->id);
<br>return response()->json([
<br>'success' => true,
<br>'message' => 'All post grabbed',
<br>'data' => [
<br>'post' => [
<br>'id' => $post->id,
<br>'content' => $post->content,
<br>'comments' => $post->comments,
<br>]
<br>]
<br>]);
<br>}
<br>}<br><br>
<img src="gambar/14.PNG">

<h3>langkah ke-4</h3>
<p>4. Buatlah <i>file CommentController.php</i> dan isilah dengan baris kode berikut</p>
<i><?php
<br>namespace App\Http\Controllers;
<br>use App\Models\Post;
<br>use Illuminate\Http\Request;
<br>class CommentController extends Controller

<br>{
<br>/**
<br>* Create a new controller instance.
<br>*
<br>* @return void
<br>*/
<br>public function __construct()
<br>{
<br>//
<br>}
<br>//
<br>public function createComment(Request $request)
<br>{
<br>$comment = Comment::create([
<br>'review' => $request->review,
<br>'postId' => $request->postId,
<br>]);
<br>return response()->json([
<br>'success' => true,
<br>'message' => 'New post created',
<br>'data' => [
<br>'comment' => $comment
<br>]
<br>]);
<br>}
<br>}<br><br>
<img src="gambar/15.PNG">

<h3>langkah ke-5</h3>
<p>5. Tambahkan baris berikut pada <i>routes/web.php</i></p>
<i><?php
<br>...
<br>$router->group(['prefix' => 'posts'], function () use ($router) {
<br>$router->post('/', ['uses' => 'PostController@createPost']);
<br>$router->get('/{id}', ['uses' => 'PostController@getPostById']);
<br>});
<br>$router->group(['prefix' => 'comments'], function () use ($router) {
<br>$router->post('/', ['uses' => 'CommentController@createComment']);
<br>});<br><br>
<img src="gambar/16.PNG">

<h3>langkah ke-6<h3>
<p>Buatlah satu <i>post</i> menggunakan <i>Postman</i></p>
<img src="gambar/17.PNG">

<h3>langkah ke-7<h3>
<p>Buatlah satu <i>comment</i> menggunakan <i>Postman</i></p>
<img src="gambar/18.PNG">

<h3>langkah ke-8<h3>
<p>Tampilkan <i>post</i> menggunakan <i>Postman</i></p>
<img src="gambar/19.PNG">

<h2>Relasi Many-to-Many</h2>
<h3>langkah ke-1</h3>
<p>1. Tambahkan fungsi <i>tags()</i> pada <i>file Post.php</i></p>
<i><?php
<br>namespace App\Models;
<br>use Illuminate\Database\Eloquent\Model;

<br>class Post extends Model
<br>{
<br>...
<br>public function tags()
<br>{
<br>return $this->belongsToMany(Tag::class, 'post_tag', 'postId', 'tagId');
<br>}
<br>}
<br></i><br><br>
<img src="gambar/20.PNG">

<h3>langkah ke-2</h3>
<p>2. Tambahkan fungsi <i>posts()</i> pada file <i>Tag.php</i></p>
<i><?php
<br>namespace App\Models;
<br>use Illuminate\Database\Eloquent\Model;

<br>class Tag extends Model
<br>{
<br>...
<br>public function posts()
<br>{
<br>return $this->belongsToMany(Tag::class, 'post_tag', 'tagId', 'postId');
<br>}
<br>}
<br><br>
<img src="gambar/21.PNG">

<h3>langkah ke-3</h3>
<p>3. Buatlah <i>file TagController.php</i> dan isilah dengan baris kode berikut</p>
<i><?php
<br>namespace App\Http\Controllers;
<br>use App\Models\Tag;
<br>use Illuminate\Http\Request;
<br>class TagController extends Controller
<br>{
<br>/**
<br>* Create a new controller instance.
<br>*
<br>* @return void
<br>*/
<br>public function __construct()
<br>{
<br>//
<br>}
<br>//
<br>public function createTag(Request $request)
<br>{
<br>$tag = Tag::create([
<br>'name' => $request->name
<br>]);
<br>return response()->json([
<br>'success' => true,
<br>'message' => 'New tag created',
<br>'data' => [
<br>'tag' => $tag
<br>]
<br>]);
<br>}
<br>}<br><br>
<img src="gambar/22.PNG">

<h3>langkah ke-4</h3>
<p>4. Tambahkan fungsi <i>addTag</i> dan <i>response tags</i> pada <i>PostController.php</i></p>
<i><?php
<br>namespace App\Http\Controllers;
<br>use App\Models\Post;
<br>use Illuminate\Http\Request;
<br>class PostController extends Controller
<br>{
<br>...
<br>public function getPostById(Request $request)
<br>{
<br>$post = Post::find($request->id);
<br>return response()->json([
<br>'success' => true,
<br>'message' => 'All post grabbed',
<br>'data' => [
<br>'post' => [
<br>'id' => $post->id,
<br>'content' => $post->content,
<br>'comments' => $post->comments,
<br>'tags' => $post->tags, //response tags
<br>]
<br>]
<br>]);
<br>}
<br>public function addTag(Request $request)
<br>{
<br>$post = Post::find($request->id);
<br>$post->tags()->attach($request->tagId);
<br>return response()->json([
<br>'success' => true,
<br>'message' => 'Tag added to post',
<br>]);
<br>}
<br>}<br><br>
<img src="gambar/23.PNG">    

<h3>langkah ke-5</h3>
<p>5. Tambahkan baris berikut pada <i>routes/web.php</i></p>
<i>$router->group(['prefix' => 'posts'], function () use ($router) {
<br>$router->post('/', ['uses' => 'PostController@createPost']);
<br>$router->get('/{id}', ['uses' => 'PostController@getPostById']);
<br>$router->put('/{id}/tag/{tagId}', ['uses' => 'PostController@getPostById']); //
<br>});
<br>...
<br>$router->group(['prefix' => 'tags'], function () use ($router) {
<br>$router->post('/', ['uses' => 'TagController@createTag']);
<br>});<br><br>

<img src="gambar/24.PNG">

<h3>langkah ke-6</h3>
<p>6. Buatlah satu <i>tag</i> menggunakan <i>Postman</i></p>
<img src="gambar/25.PNG">

<h3>langkah ke-7</h3>
<p>7. Tambahkan <i>tag</i> “jadul” pada <i>post</i> “disana engkau berdua”</p>
<img src="gambar/26.PNG">

<h3>langkah ke-8</h3>
<p>8. Tampilkan <i>post</i> “disana engkau berdua” menggunakan <i>Postman</i></p>
<img src="gambar/27.PNG">

<h3>langkah ke-9</h3>
<p>9. Buatlah postingan “tanpamu apa artinya” menggunakan <i>Postman</i></p>
<img src="gambar/28.PNG">

<h3>langkah ke-10</h3>
<p>10. Tambahkan <i>tag</i> “jadul” pada postingan “tanpamu apa artinya”</p>
<img src="gambar/29.PNG">

<h3>langkah ke-11</h3>
<p>11. Buatlah <i>tag</i> “lagu” menggunakan <i>Postman</i></p>
<img src="gambar/30.PNG">

<h3>langkah ke-12</h3>
<p>12. Tambahkan <i>tag</i> “lagu” pada postingan “tanpamu apa artinya”</p>
<img src="gambar/31.PNG">

<h3>langkah ke-13</h3>
<p>13. Tampilkan Tampilkan <i>post</i> pertama</i></p>
<img src="gambar/32.PNG">

<h3>langkah ke-14</h3>
<p>14. Tampilkan <i>Tampilkan <i>post</i> kedu</i></p>
<img src="gambar/33.PNG">