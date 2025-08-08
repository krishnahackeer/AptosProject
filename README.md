💸 Aptos Tipping Module
📜 Description
The Aptos Tipping Module is a Move-based smart contract that enables users to send and receive tips in AptosCoin. It introduces a TipBox resource for each user, allowing them to track the total amount of tips received. This module is ideal for creators, developers, and service providers who want to accept micro-payments or donations on-chain.

🎯 Vision
To create a seamless and transparent tipping mechanism on the Aptos blockchain that empowers peer-to-peer appreciation and micro-reward systems. By leveraging AptosCoin and Move’s resource-oriented programming, the module ensures secure and auditable transactions.

🚀 Future Scope
UI Integration: Build a frontend interface for users to send and view tips.

Multi-Coin Support: Extend functionality to support other coin types.

Analytics Dashboard: Visualize tipping history, top tippers, and trends.

Access Control: Add permission layers for who can initialize or withdraw from TipBoxes.

Event Emission: Emit custom events for tipping actions to improve traceability.

Code :
module MyModule::Tipping {
    use aptos_framework::coin;
    use aptos_framework::aptos_coin::AptosCoin;

    TipBox resource storing total tips received
    struct TipBox has key, store {
        total_received: u64,
    }

    Creates a TipBox for a user to receive tips
    public fun initialize_tipbox(account: &signer) {
        move_to(account, TipBox { total_received: 0 });
    }

  Sends a tip in AptosCoin to a recipient's TipBox
    public fun send_tip(sender: &signer, recipient: address, amount: u64) acquires TipBox {
        let tip = coin::withdraw<AptosCoin>(sender, amount);
        coin::deposit<AptosCoin>(recipient, tip);

        let tipbox = borrow_global_mut<TipBox>(recipient);
        tipbox.total_received = tipbox.total_received + amount;
    }
}



''' 
Transaction submitted: https://explorer.aptoslabs.com/txn/0x0a98d3a86869a87c798ecefe168979b4eeca288d6a6efc44828b8caa8f9b037b?network=devnet
{
  "Result": {
    "transaction_hash": "0x0a98d3a86869a87c798ecefe168979b4eeca288d6a6efc44828b8caa8f9b037b",
    "gas_used": 1948,
    "gas_unit_price": 100,
    "sender": "af4e72560798bdbfd8592e31a5818a6380da348ead111979df9436646ef63f64",
    "sequence_number": 0,
    "replay_protector": {
      "SequenceNumber": 0
    },
    "success": true,
    <img width="1393" height="913" alt="image" src="https://github.com/user-attachments/assets/b46e9017-dbdd-44d5-add7-32f773365446" />
    "timestamp_us": 1754650121868368,
    "version": 27893030,
    "vm_status": "Executed successfully"
  }
} '''
