pragma solidity 0.4.17;
contract lesson2 {
    mapping (address => address) public BorrowerAddr;
    mapping (address => int) public ReturnSum;

    function Borrow(address _BorrowerAddr, int _BorrowAmount) public returns (bool, string, int) {
        ReturnSum[msg.sender] = _BorrowAmount;
        BorrowerAddr[msg.sender] = _BorrowerAddr;
        return (true, 'Now I have a loan :(', _BorrowAmount);
}


    function ReFund(address _ReFundAddr, int _ReFundAmount) public returns(bool, string){
        ReturnSum[_ReFundAddr] -= _ReFundAmount;
        return (true, "My debt become little bit smaller");
    }
}
