pragma solidity 0.4.17;

contract Borrower 
{
    address owner;
    mapping (address => uint) private Ledger;
    event EventMessage(string MessageText);
    
    function BorrowSum (uint BorrowAmount) public 
    {
        if (Ledger[msg.sender] + BorrowAmount > Ledger[msg.sender] || Ledger[msg.sender] == 0)
        {
            Ledger[msg.sender] = Ledger[msg.sender] + BorrowAmount;
            EventMessage ("Successful borrow");
            return;
        }
        EventMessage("Borrow ammount not correct!");
        return;
    }
    
    function ReFundSum (address user, uint ReFundAmount) public 
    {
        if (msg.sender == owner) 
        {
            if (Ledger[user] - ReFundAmount < Ledger[user] || Ledger[user] - ReFundAmount == 0)
            {
                Ledger[user] = Ledger[user] - ReFundAmount;
                EventMessage ("Successful refund");
                return;
            }
            EventMessage("ReFund ammount not correct!");
            return;
        }
        EventMessage ("Refund Not allowed");
        return;
    }
    
    function getAmmount (address user) public returns (uint) 
    {
        if (user == msg.sender) 
        {
            return (Ledger[user]);
        }
        else if (msg.sender == owner) 
        {
            return (Ledger[user]);
        }
        EventMessage("You have no permittion to view balance");
        return;
    }
}
