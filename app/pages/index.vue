<template>
  <div>
    <h1>Welcome to the homepage</h1>
    <div class="meeting-rooms">
      <h2>Available Meeting Rooms</h2>

      <ul v-if="rooms.length > 0">
        <li v-for="room in rooms" :key="room.id" class="room-card">
          <div class="room-info">
            <h3>{{ room.name }}</h3>
            <p>Capacity: {{ room.capacity }}</p>
            <p v-if="room.booked" class="booked">Status: Booked</p>
            <p v-else class="available">Status: Available</p>
          </div>
          <button :disabled="room.booked" @click="bookRoom(room.id)">
            {{ room.booked ? "Booked" : "Book Room" }}
          </button>
        </li>
      </ul>

      <p v-else>No meeting rooms available.</p>
    </div>
    <AppAlert> This is an auto-imported component </AppAlert>
  </div>
</template>

<script setup>
import { reactive } from "vue";

// Sample room data
const rooms = reactive([
  { id: 1, name: "Conference Room A", capacity: 10, booked: false },
  { id: 2, name: "Meeting Room B", capacity: 6, booked: false },
  { id: 3, name: "Board Room C", capacity: 20, booked: true },
]);

// Booking function
function bookRoom(roomId) {
  const room = rooms.find((r) => r.id === roomId);
  if (room && !room.booked) {
    room.booked = true;
    alert(`You have booked ${room.name}`);
  }
}
</script>

<style scoped>
.meeting-rooms {
  max-width: 600px;
  margin: auto;
  font-family: Arial, sans-serif;
}
.room-card {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #f5f5f5;
  padding: 1rem;
  margin-bottom: 1rem;
  border-radius: 8px;
}
.room-info h3 {
  margin: 0;
}
.booked {
  color: red;
}
.available {
  color: green;
}
button[disabled] {
  background: #ccc;
  cursor: not-allowed;
}
</style>
