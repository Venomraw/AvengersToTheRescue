# CAN Bus

# Tools

- Wireshark
- Excel
- jsconsole

## Using Wireshark

Will be using wireshark to analyze CAN bus data

Open wireshark

Click file and click candump.pcap you downloaded

Right click on ID and select Apply as Column or Ctrl+Shift+I

In the left bottom corner, click Data Apply as Column or Ctrl+Shift+I

Click file on the top and Export Packet Dissections As CSV

## Using Excel

We be using excel to find specific information from the CAN bus data

### Finding Unique CAN Bus IDS

Open the file in excel

Click or highlight the Info column

On the top click Data and find data tools

On data tools click Remove Duplicates 

Make sure the Info Column is highlighted

Once done, the unqie values will be provide, but make sure to minus it by 1 for the actual value

### Counting Repeated IDS

Undo the changes made for the remove duplicates

Ctrl+F and type 589 on Find what:

Click find all

On the bottom left it should give you the amount of times it has been repeated.

## Using jsconsole

For this case, use jsconsole to help with calculation

### Preparation

Highlight the ID column and click filter

Click the down arrow next to the ID column

Unselect all and search for 589

Once filter, click or highlight the Data column

Click Sort from A-Z

Scroll down and find the maximum value in Data column and copy it

### Finding the Maximum Speed in Mph

Split the copy data value into seperate columns like this
`00 00 00 0c a8`

This is the code will be using to help assist with the calculation( Dont input this in jscode)

```
int speed_id = 589;
int speed_pos = 3;
struct canfd_frame frame;

while (PollEvent(&event) != 0) {
    read_data(&event, &frame);
    if (frame.can_id == speed_id) {
        double speed = frame->data[speed_pos] << 8;
        speed += frame->data[speed_pos + 1];
        speed = speed / 100;
        speed = speed * 0.6213751;
        update_speed(speed);
    }
}
```
The seperate columns that is split from the data value copy earlier goes from 0-4 in columns

Since the speed pos is 3, it will be in column 3 of the data value which is `0c` of `00 00 00 0c a8`

So in jsconsole input `speed = 0x0c << 8`

0x0c converts hexadecimal to decimal

For this area in the code here `speed += frame->data[speed_pos + 1]`, you must add 1 to the speed pos

Speed pos is 4, which means it in column 4 of the data value which is `a8` of `00 00 00 0c a8`

Input `speed += 0xa8` in jsconsole

Next you would divide the speed by a 100 so input `speed = speed / 100`

Last input `speed = speed * 0.6213751` to convert kph to mph

The final value should be shown on jsconsole when finding the maximum speed in mph


Answers

```
1. 36
2. 352
3. 20.133
````