# website-personal
import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { ShoppingCart, Star } from "lucide-react";

const products = [
  { id: 1, name: "Lipstick Matte", price: 120000, category: "Makeup", image: "lipstick.jpg", reviews: ["Sangat bagus!", "Warna tahan lama"] },
  { id: 2, name: "Dress Elegan", price: 350000, category: "Fashion", image: "dress.jpg", reviews: ["Cantik dan nyaman"] },
  { id: 3, name: "Parfum Wanita", price: 250000, category: "Parfum", image: "parfum.jpg", reviews: ["Wangi lembut", "Tahan lama"] },
  { id: 4, name: "Skincare Premium", price: 500000, category: "Skincare", image: "skincare.jpg", reviews: ["Kulit jadi lebih sehat"] }
];

export default function Shop() {
  const [cart, setCart] = useState([]);
  const [category, setCategory] = useState("All");

  const addToCart = (product) => {
    setCart([...cart, product]);
  };

  const checkout = () => {
    alert("Checkout berhasil! Terima kasih telah berbelanja.");
    setCart([]);
  };

  const filteredProducts = category === "All" ? products : products.filter(p => p.category === category);

  return (
    <div className="p-4">
      <h1 className="text-3xl font-bold text-center mb-4">Toko Kecantikan & Fashion</h1>
      
      <div className="flex gap-2 mb-4">
        {['All', 'Makeup', 'Fashion', 'Parfum', 'Skincare'].map(cat => (
          <Button key={cat} onClick={() => setCategory(cat)} className={`bg-${category === cat ? 'pink-600' : 'gray-300'} px-4 py-2 rounded-md`}>
            {cat}
          </Button>
        ))}
      </div>
      
      <div className="grid grid-cols-2 md:grid-cols-4 gap-4">
        {filteredProducts.map((product) => (
          <Card key={product.id} className="p-2 shadow-lg">
            <img src={product.image} alt={product.name} className="w-full h-40 object-cover rounded-md" />
            <CardContent>
              <h2 className="text-lg font-semibold">{product.name}</h2>
              <p className="text-pink-600 font-bold">Rp {product.price.toLocaleString()}</p>
              <Button onClick={() => addToCart(product)} className="mt-2 w-full bg-pink-500">
                <ShoppingCart size={16} className="mr-2" /> Tambah ke Keranjang
              </Button>
              <div className="mt-2">
                <h3 className="text-sm font-bold">Ulasan:</h3>
                {product.reviews.map((review, index) => (
                  <p key={index} className="text-gray-600 flex items-center"><Star size={12} className="text-yellow-400 mr-1" /> {review}</p>
                ))}
              </div>
            </CardContent>
          </Card>
        ))}
      </div>
      
      <div className="mt-6 p-4 bg-gray-100 rounded-md">
        <h2 className="text-xl font-bold">Keranjang Belanja</h2>
        {cart.length > 0 ? (
          <>
            {cart.map((item, index) => (
              <p key={index} className="text-gray-700">{item.name} - Rp {item.price.toLocaleString()}</p>
            ))}
            <Button onClick={checkout} className="mt-4 bg-green-500 w-full">Checkout</Button>
          </>
        ) : (
          <p className="text-gray-500">Keranjang masih kosong.</p>
        )}
      </div>
    </div>
  );
}
