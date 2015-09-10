# Import to Your Own Project #

  1. Add new calendar activity to your own AndroidManifest.xml
```
<activity android:name="com.exina.android.calendar.CalendarActivity">
    
    <intent-filter>
        <action android:name="android.intent.action.PICK" />
        <category android:name="android.intent.category.DEFAULT" />
        <data android:mimeType="vnd.android.cursor.dir/vnd.exina.android.calendar.date" />
    </intent-filter>
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <data android:mimeType="vnd.android.cursor.dir/vnd.exina.android.calendar.date" />
    </intent-filter>
</activity>
```
  1. Copy source files to your own project's src folder
```
com/exina/android/calendar/CalendarActivity.java
com/exina/android/calendar/CalendarView.java
com/exina/android/calendar/Cell.java
```
  1. Copy following resource files to your project's res folder
```
layout: main.xml
drawable: background.png, calendar_week.png, typeb_calendar_today.png
values: dimens.xml
```
# Display Calendar View #
Simply call calendar view with Intent, like:
```
startActivity(new Intent(Intent.ACTION_VIEW).setDataAndType(null, CalendarActivity.MIME_TYPE));
```
# Using Calendar View to Pick Up a Date #
By using startActivityForResult to call calendar view and expect a result.
```
// 1) start calendar view
startActivityForResult(new Intent(Intent.ACTION_PICK).setDataAndType(null, CalendarActivity.MIME_TYPE), 100);

// 2) implement your own onActivityResult method to handle returned date
@Override
public void onActivityResult(int requestCode, int resultCode, Intent data) {
    if(resultCode==RESULT_OK) {
        int year = data.getIntExtra("year", 0);   // get number of year
        int month = data.getIntExtra("month", 0); // get number of month 0..11
        int day = data.getIntExtra("day", 0);     // get number of day 0..31

        // format date and display on screen
        final Calendar dat = Calendar.getInstance();
        dat.set(Calendar.YEAR, year);
        dat.set(Calendar.MONTH, month);
        dat.set(Calendar.DAY_OF_MONTH, day);
        
        // show result
        SimpleDateFormat format = new SimpleDateFormat("yyyy MMM dd");
        Toast.makeText(TestActivity.this, format.format(dat.getTime()), Toast.LENGTH_LONG).show();
                
    }
}

```