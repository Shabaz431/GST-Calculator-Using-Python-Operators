# GST Calculator Using Python Operators

VALID_SLABS = [0, 0.25, 3, 5, 12, 18, 28]   # Indian GST slabs (%)

def get_float(prompt):
    """Keep asking until the user enters a valid positive number."""
    while True:
        try:
            value = float(input(prompt))
            if value >= 0 and not value != value:   # comparison + logical operators
                return value
            print("Please enter a non-negative number.")
        except ValueError:
            print("Invalid input. Enter a number.")

def get_slab():
    while True:
        rate = get_float(f"Enter GST rate {VALID_SLABS}: ")
        if rate in VALID_SLABS:                      # membership operator
            return rate
        print("Not a valid GST slab. Try again.")

def add_gst(price, rate):
    gst = price * rate / 100                         # arithmetic operators
    total = price + gst
    return gst, total

def remove_gst(total, rate):
    base = total * 100 / (100 + rate)
    gst = total - base
    return gst, base

def show_bill(base, gst, total, rate):
    cgst = sgst = gst / 2
    print("\n" + "=" * 32)
    print(f"{'Base Price':<15}: ₹{base:>12,.2f}")
    print(f"{'CGST (' + str(rate/2) + '%)':<15}: ₹{cgst:>12,.2f}")
    print(f"{'SGST (' + str(rate/2) + '%)':<15}: ₹{sgst:>12,.2f}")
    print(f"{'Total GST':<15}: ₹{gst:>12,.2f}")
    print(f"{'Final Amount':<15}: ₹{total:>12,.2f}")
    print("=" * 32)

def main():
    print("===== GST CALCULATOR =====")
    grand_total = 0                                   # assignment operators
    count = 0

    while True:
        print("\n1. Add GST to price\n2. Remove GST from price\n3. Exit")
        choice = input("Choose (1/2/3): ").strip()

        if choice == "1":
            price = get_float("Enter original price: ₹")
            rate = get_slab()
            gst, total = add_gst(price, rate)
            show_bill(price, gst, total, rate)
            grand_total += total
            count += 1
        elif choice == "2":
            total = get_float("Enter price including GST: ₹")
            rate = get_slab()
            gst, base = remove_gst(total, rate)
            show_bill(base, gst, total, rate)
            grand_total += total
            count += 1
        elif choice == "3":
            break
        else:
            print("Invalid choice.")

    if count > 0:
        print(f"\nCalculations done: {count} | Combined total: ₹{grand_total:,.2f}")
    print("Thank you!")

if __name__ == "__main__":
    main()
