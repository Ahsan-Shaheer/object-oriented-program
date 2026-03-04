#include <iostream>
#include <string>
using namespace std;

class Ride{
protected:
    string passengerName;
    int rideID;
    double baseFare;

public:
    Ride(string name, int id, double fare) : passengerName(name),rideID(id),baseFare(fare) {}

    virtual void displayRideDetails() {
        cout << "Passenger Name is : " <<passengerName<<endl;
        cout << "Ride ID is : " <<rideID<<endl;
        cout << "Base Fare is : " <<baseFare<<endl;
    }

    
    virtual double calculateFare() = 0; 
};

class EconomyRide:public Ride {
private:
    double distanceKm;

public:
    EconomyRide(string name, int id, double fare, double dist) 
        : Ride(name, id, fare), distanceKm(dist) {}

    double calculateFare() override {
        
        return baseFare + (distanceKm * 8);
    }

    void displayRideDetails() override {
        cout << "(Economy Ride Details are)" << endl;
        Ride::displayRideDetails();
        cout << "Distance is: " << distanceKm << " km" << endl;
        cout << "Total Fare is : " << calculateFare() << endl;
    }
};
class LuxuryRide : public Ride {
private:
    double distanceKm;
    double serviceCharge;
public:
    LuxuryRide(string name, int id, double fare, double dist, double service) 
        : Ride(name, id, fare), distanceKm(dist), serviceCharge(service) {}
    double calculateFare() override {
        return baseFare + (distanceKm * 12) + serviceCharge;
    }

    void displayRideDetails() override {
        cout << "(Luxury Ride Details are)" << endl;
        Ride::displayRideDetails();
        cout << "Distance is : " << distanceKm << " km" <<endl;
        cout << "Service Charge are: " << serviceCharge <<endl;
        cout << "Total Fare is : " << calculateFare() <<endl;   
    }
};

int main() {
    
    EconomyRide ecoRide("ahad", 200, 101.0, 14.0);
    LuxuryRide luxRide("Ali", 500, 510.0, 25.0, 260.0);
    ecoRide.displayRideDetails();
    luxRide.displayRideDetails();

    return 0;
}
