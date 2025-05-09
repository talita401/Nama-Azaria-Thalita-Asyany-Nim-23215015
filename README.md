// app/Http/Controllers/CartController.php
use Illuminate\Http\Request;
use App\Models\Product;

class CartController extends Controller
{
    public function add(Request $request, $id)
    {
        $product = Product::find($id);
        $cart = session()->get('cart', []);
        $cart[$id] = [
            "name" => $product->name,
            "quantity" => 1,
            "price" => $product->price
        ];
        session()->put('cart', $cart);
        return redirect()->back()->with('success', 'Product added to cart!');
    }
}
