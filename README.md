import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";

export default function KakesByKendall() {
  const [date, setDate] = useState("");
  const [guests, setGuests] = useState("");
  const [step, setStep] = useState(1);
  const [message, setMessage] = useState("");

  const [packageType, setPackageType] = useState("");
  const [cakeBase, setCakeBase] = useState("");
  const [showCustomCake, setShowCustomCake] = useState(false);
  const [showCustomTopping, setShowCustomTopping] = useState(false);

  const [bookedDates] = useState([
    "2026-06-14",
    "2026-06-20",
    "2026-07-04",
  ]);

  const checkAvailability = () => {
    if (!date) return;

    if (bookedDates.includes(date)) {
      setMessage("Sorry, that date is already booked. Please choose another.");
      setStep(1);
    } else {
      setMessage("Great news! Your date looks available 🎉");
      setStep(2);
    }
  };

  const submitLead = () => {
    setStep(3);
  };

  const cakeFlavorLimit = packageType === "Signature" ? 2 : 3;
  const icingFlavorLimit = packageType === "Signature" ? 2 : 3;

  return (
    <div className="min-h-screen bg-black text-white">

      <section className="relative text-white">
        <div
          className="absolute inset-0 bg-center bg-cover"
          style={{ backgroundImage: "url('/cart.jpg')" }}
        />

        <div className="absolute inset-0 bg-black/70" />

        <div className="relative text-center py-32 px-6 max-w-4xl mx-auto">
          <img
            src="/logo.png"
            alt="Kakes by Kendall Logo"
            className="mx-auto mb-10 w-64 md:w-80 drop-shadow-[0_0_45px_rgba(255,0,140,1)]"
          />

          <h1 className="text-4xl md:text-6xl font-bold mb-6">
            The Cake Cart Experience Your Guests Will Never Forget
          </h1>

          <p className="text-lg md:text-xl mb-10 text-gray-200">
            Interactive dessert experience for weddings, birthdays, and unforgettable events.
          </p>

          <Card className="max-w-xl mx-auto rounded-2xl bg-black/80 border border-pink-500 shadow-[0_0_25px_rgba(255,0,140,0.6)]">
            <CardContent className="p-6 space-y-4 text-white">

              {step === 1 && (
                <>
                  <h2 className="text-xl font-semibold text-pink-400">Check Your Event Date</h2>

                  <input
                    type="date"
                    value={date}
                    onChange={(e) => setDate(e.target.value)}
                    className="w-full bg-black border border-pink-500 p-3 rounded-xl"
                  />

                  <input
                    type="number"
                    placeholder="Guest Count"
                    value={guests}
                    onChange={(e) => setGuests(e.target.value)}
                    className="w-full bg-black border border-pink-500 p-3 rounded-xl"
                  />

                  <Button
                    onClick={checkAvailability}
                    className="w-full text-lg rounded-xl bg-pink-500 hover:bg-pink-600 shadow-[0_0_20px_rgba(255,0,140,0.8)]"
                  >
                    Check Availability
                  </Button>

                  {message && <p className="text-sm text-pink-300">{message}</p>}
                </>
              )}

              {step === 2 && (
                <>
                  <h2 className="text-2xl font-semibold text-pink-400">Event Details</h2>

                  <input
                    type="text"
                    placeholder="Full Name"
                    className="w-full bg-black border border-pink-500 p-3 rounded-xl"
                  />

                  <input
                    type="email"
                    placeholder="Email Address"
                    className="w-full bg-black border border-pink-500 p-3 rounded-xl"
                  />

                  <input
                    type="tel"
                    placeholder="Phone Number"
                    className="w-full bg-black border border-pink-500 p-3 rounded-xl"
                  />

                  <div className="text-left">
                    <p className="text-pink-300 mb-2">Select Package</p>

                    <select
                      value={packageType}
                      onChange={(e) => setPackageType(e.target.value)}
                      className="w-full bg-black border border-pink-500 p-3 rounded-xl"
                    >
                      <option value="">Choose Package</option>
                      <option value="Signature">Signature Cart</option>
                      <option value="Luxury">Luxury Event</option>
                      <option value="Custom">Custom Experience</option>
                    </select>

                    {packageType === "Signature" && (
                      <p className="text-sm text-gray-300 mt-2">
                        Starting at $325 • Includes 24 cake pieces • 1.5 hour service • 1 attendant
                      </p>
                    )}

                    {packageType === "Luxury" && (
                      <p className="text-sm text-gray-300 mt-2">
                        Starting at $650 • Includes 50 cake pieces • 1.5 hour service • 1 attendant
                      </p>
                    )}
                  </div>

                  {packageType && (
                    <>

                      <div className="text-left">
                        <p className="text-pink-300 mb-2">Cake Flavors (select up to {cakeFlavorLimit})</p>

                        <select
                          value={cakeBase}
                          onChange={(e) => {
                            setCakeBase(e.target.value);
                            setShowCustomCake(e.target.value === "Custom");
                          }}
                          className="w-full bg-black border border-pink-500 p-3 rounded-xl"
                        >
                          <option>Chocolate</option>
                          <option>Vanilla</option>
                          <option>Red Velvet</option>
                          <option>Funfetti</option>
                          <option>Custom</option>
                        </select>

                        {showCustomCake && (
                          <input
                            type="text"
                            placeholder="Enter custom cake flavor"
                            className="mt-2 w-full bg-black border border-pink-500 p-3 rounded-xl"
                          />
                        )}
                      </div>

                      <div className="text-left">
                        <p className="text-pink-300 mb-2">Icing Flavors (select up to {icingFlavorLimit})</p>

                        <select className="w-full bg-black border border-pink-500 p-3 rounded-xl">
                          <option>American Buttercream</option>
                          <option>Chocolate</option>
                          <option>Whipped</option>
                        </select>
                      </div>

                      <div className="text-left">
                        <p className="text-pink-300 mb-2">Select Toppings</p>

                        <div className="grid grid-cols-2 gap-2 text-sm">
                          {[
                            "Chocolate Chips",
                            "M&M's",
                            "Strawberries",
                            "Strawberry Crunch",
                            "Graham Crackers",
                            "Oreos",
                            "Chips Ahoy",
                            "Marshmallows",
                            "Shaved Coconut",
                            "Rainbow Sprinkles",
                            "Chocolate Jimmies",
                            "Hershey's Chocolate",
                            "Fruity Pebbles",
                            "Lucky Charms",
                            "Biscoff Cookie"
                          ].map((topping) => (
                            <label key={topping} className="flex items-center gap-2">
                              <input type="checkbox" className="accent-pink-500" />
                              {topping}
                            </label>
                          ))}
                        </div>

                        <label className="flex items-center gap-2 mt-3">
                          <input
                            type="checkbox"
                            onChange={(e) => setShowCustomTopping(e.target.checked)}
                            className="accent-pink-500"
                          />
                          Other topping
                        </label>

                        {showCustomTopping && (
                          <input
                            type="text"
                            placeholder="Enter additional topping"
                            className="mt-2 w-full bg-black border border-pink-500 p-3 rounded-xl"
                          />
                        )}
                      </div>

                    </>
                  )}

                  <Button
                    onClick={submitLead}
                    className="w-full text-lg rounded-xl bg-pink-500 hover:bg-pink-600 shadow-[0_0_20px_rgba(255,0,140,0.8)]"
                  >
                    Submit Booking Request
                  </Button>
                </>
              )}

              {step === 3 && (
                <>
                  <h2 className="text-xl font-semibold text-pink-400">Request Sent ✨</h2>
                  <p className="text-gray-300">
                    Thanks for your interest in the Kakes by Kendall Cake Cart! We'll review your event and confirm availability shortly.
                  </p>
                </>
              )}

            </CardContent>
          </Card>
        </div>
      </section>

      <section className="py-24 px-6 text-center max-w-5xl mx-auto">
        <h2 className="text-4xl font-bold mb-14 text-pink-400">How The Cake Cart Experience Works</h2>

        <div className="grid md:grid-cols-3 gap-10 text-left">
          <Card className="bg-black border border-pink-500 rounded-2xl">
            <CardContent className="p-8">
              <h3 className="text-xl font-semibold text-pink-300 mb-3">1. Choose Your Cake</h3>
              <p className="text-gray-300">Select your favorite cake flavors and icing combinations for your event.</p>
            </CardContent>
          </Card>

          <Card className="bg-black border border-pink-500 rounded-2xl">
            <CardContent className="p-8">
              <h3 className="text-xl font-semibold text-pink-300 mb-3">2. Pick Your Toppings</h3>
              <p className="text-gray-300">Guests customize their dessert with fun toppings like Oreos, strawberries, sprinkles, cereal and more.</p>
            </CardContent>
          </Card>

          <Card className="bg-black border border-pink-500 rounded-2xl">
            <CardContent className="p-8">
              <h3 className="text-xl font-semibold text-pink-300 mb-3">3. We Serve Your Guests</h3>
              <p className="text-gray-300">Our team brings the cake cart to your event and serves guests fresh cake creations for an unforgettable experience.</p>
            </CardContent>
          </Card>
        </div>
      </section>

      <section className="py-24 px-6 text-center max-w-5xl mx-auto">
        <h2 className="text-4xl font-bold mb-14 text-pink-400">Event Packages</h2>

        <div className="grid md:grid-cols-3 gap-8">
          <Card className="rounded-2xl bg-black border border-pink-500">
            <CardContent className="p-8">
              <h3 className="text-xl font-semibold mb-2 text-pink-300">Signature Cart</h3>
              <p className="text-4xl font-bold mb-4 text-amber-300">Starting at $325</p>
              <p className="text-gray-300">24 pieces of cake • 1.5 hour service • 1 attendant • Perfect for smaller parties</p>
            </CardContent>
          </Card>

          <Card className="rounded-2xl bg-black border-2 border-pink-500 shadow-[0_0_25px_rgba(255,0,140,0.6)]">
            <CardContent className="p-8">
              <h3 className="text-xl font-semibold mb-2 text-pink-300">Luxury Event</h3>
              <p className="text-4xl font-bold mb-4 text-amber-300">Starting at $650</p>
              <p className="text-gray-300">50 pieces of cake • 1.5 hour service • 1 attendant • Most popular for larger events</p>
            </CardContent>
          </Card>

          <Card className="rounded-2xl bg-black border border-pink-500">
            <CardContent className="p-8">
              <h3 className="text-xl font-semibold mb-2 text-pink-300">Custom Experience</h3>
              <p className="text-4xl font-bold mb-4 text-amber-300">Custom Quote</p>
              <p className="text-gray-300">Fully customized cake cart experience.</p>
            </CardContent>
          </Card>
        </div>
      </section>

      <footer className="bg-black text-center py-8 text-gray-400">
        <p>Kakes by Kendall • Luxury Cake Cart Experience</p>
      </footer>

    </div>
  );
}
